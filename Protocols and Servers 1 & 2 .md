# Protocols and Servers 1 & 2 

![1727286948393](https://github.com/user-attachments/assets/c4fd78f6-949a-4475-83a8-74c7dcb8e2a4)



![1727286948331](https://github.com/user-attachments/assets/6a785adb-4ab3-462b-a645-6f6fc926e676)





attacks against login systems can be carried out efficiently using a tool, such as THC Hydra combined with a suitable word list. Mitigation against such attacks can be sophisticated and depends on the target system. A few of the approaches include:

Password Policy: Enforces minimum complexity constraints on the passwords set by the user.

Account Lockout: Locks the account after a certain number of failed attempts.

Throttling Authentication Attempts: Delays the response to a login attempt. A couple of seconds of delay is tolerable for someone who knows the password, but they can severely hinder automated tools.

Using CAPTCHA: Requires solving a question difficult for machines. It works well if the login page is via a graphical user interface (GUI). (Note that CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.)

Requiring the use of a public certificate for authentication. This approach works well with SSH, for instance.

Two-Factor Authentication: Ask the user to provide a code available via other means, such as email, smartphone app, or SMS.

There are many other approaches that are more sophisticated or might require some established knowledge about the user, such as IP-based geolocation.
