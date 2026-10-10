
<img width="1022" height="319" alt="image" src="https://github.com/user-attachments/assets/888cef2f-1c58-4ed5-98b2-137c8a40c443" />


***Task 1 Introduction***

In this room, we'll dive into different session types and how to investigate several log types at the application level to identify compromise.


##### Learning Objectives###

- Understand log types to perform application-level forensics
- Identify key behaviours that lead to session compromise
- Build alerting and detection capabilities tailored to application-level logs



***Task 2  Recap: Session & JWT***


***JWT and Tokens***

You might have heard of JSON Web Tokens (JWT), which are commonly seen in modern web applications. JWT is an open [standard(opens in new tab)](https://www.rfc-editor.org/rfc/rfc7519) used for authentication and authorisation. JWT is stateless because session information is stored on the client side and not on the backend. The structure is as follows:



<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/90f39ee1-2152-4956-8cda-a14838e2cca7" />


1.Header: Dictates the algorithm used for signing, usually RSA.
2.Payload: Contains information about the user, like role, session ID, or when the token expires.
3.Signature: Used to check if the token has been tampered with.


***Task 3 Decoding and Inspecting Tokens***

**Inspection Time**


By now, you should be familiar with session tokens, JWTs, and the ecosystems they inhabit. Let's dissect them to better understand how to inspect them and where to find them





<img width="1220" height="1080" alt="image" src="https://github.com/user-attachments/assets/de3db734-2c80-4979-b6d0-93401eeb5b84" />



**Web Server Logs**

In web server logs, like in NGINX or Apache, they will look slightly different:

`[22/Jul/2025:14:12:03 +0000] "GET /admin HTTP/1.1" 200 342 "-" "Mozilla/5.0" "sessionid=abcmewomeow456..."`


**Application Logs**

Application logs, like Django or Flask, might log the activity like this:

`[INFO] [14:12:03] User login successful. sessionid=abc123def456... assigned to user: FluffyCat`

With these logs, you can match the `sessionid` to a specific user and action in the app. In a forensic investigation, this is useful for mapping access and privilege escalation while building your timeline



![[Pasted image 20260708193657.png]]






![[Pasted image 20260708213028.png]]



![[Pasted image 20260708213203.png]]

![[Pasted image 20260708213248.png]]

![[Pasted image 20260708213349.png]]

![[Pasted image 20260708213443.png]]



![[Pasted image 20260708213600.png]]

![[Pasted image 20260708213705.png]]

![[Pasted image 20260708213747.png]]

![[Pasted image 20260708213828.png]]



**Decoding a JWT token**

You can use [jwt.io(opens in new tab)](https://jwt.io/) to decode tokens. Let's take a look at this sample token:

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30`

As discussed in the previous section, JWT consists of 3 base64 encoded sections:

<Header>.<Payload>.<Signature>





**Task 4: Session Forensics, Log Investigation**

## Scenario##



An incident was triggered recently at TryFlufMe (TFM). It seems some weird activity was happening in TFM's internal admin portal. SecOps has reached out to you, a seasoned Application Security Engineer, asking to collaborate during the incident investigation as they need advice on where to start. After reviewing endpoint logs, they have hit a wall. You have asked them for application and server logs, browser dumps and anything else they could find. You can find the logs by downloading them from the task files. Alternatively, they can be found in the "Session Forensics Logs" directory in the attackbox. The files provided are:

- `webserver.log` Tracks incoming HTTP requests to the web server. They show a user making standard requests using a legitimate token and continuing browsing behaviour with a forged token (to blend in).
- `app.log` Application-level logs from the backend. It shows tokens being validated with the role user. Then, suddenly, a warning: a mismatch with known permissions. Followed by access logs showing high-privilege features being accessed.
- `idp.log` Logs from the Identity Provider (IDP). They show every token ever issued to the user with the role user. Upon reviewing, no admin tokens were ever legitimately issued.
- `browser_dump.txt` A local forensic browser dump from a suspected infected user device. It shows a token stored in localStorage. However, something doesn't seem right here.
