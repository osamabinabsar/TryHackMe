# t2

## Making a Decision

While it is confusing to differentiate 
between TPs and FPs, it is very crucial to get it right. If a TP is 
falsely classified as an FP, it can lead to a significant impact from a 
missed cyber attack. If an FP is falsely classified as a TP, precious 
time will be spent focusing on the FP, which might lead to less focus on
 an actual attack. So, how exactly do we ensure that we perform this 
crucial job effectively? We can use the below pointers to guide us.

!https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730369772259.png

**Using the SOC Superpower**

The SOC
 has a superpower. When they are unsure whether an activity is performed
 by a malicious actor or a legitimate user, they can just confirm with 
the user. This privilege is not available to the attacker. A SOC
 analyst, on the other hand, can just send an email or call the relevant
 person to get confirmation of a certain activity. In mature 
organisations, any changes that might trigger an alert in the SOC
 often require Change Requests to be created and approved through the IT
 change management process. Depending on the process, the SOC
 team can ask the users to share Change Request details for 
confirmation. Surely, if it is a legitimate and approved activity, it 
must have an approved Change Request.

**Context**

While it might seem like using the SOC superpower makes things super easy, that is not always the case. There are cases which can act as Kryptonite to the SOC superpower:

- If an organisation doesn't have a change request process in place.
- The performed activity was outside the scope of the change request or was different from that of the approved change request.
- The activity triggered an alert, such as copying files to a certain
location, uploading a file to some website, or a failed login to a
system.
- An insider threat performed an activity they are not authorised to perform, whether intentionally or unintentionally.
- A user performed a malicious activity via social engineering from a threat actor.

In such scenarios, it is very important for the SOC
 analyst to understand the context of the activity and make a judgement 
call based on their analysis skills and security knowledge. While doing 
so, the analyst can look at the past behaviour of the user or the 
prevalence of a certain event or artefact throughout the organisation or
 a certain department. For example, if a certain user from the network 
team is using Wireshark, there is a chance that other users from the 
same team also use Wireshark. However, Wireshark seen on a machine 
belonging to someone from HR or finance should rightfully raise some 
eyebrows.

!https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730370031153.png

**Correlation**

When
 building the context, the analyst must correlate different events to 
make a story or a timeline. Correlation entails using the past and 
future events to recreate a timeline of events. When performing 
correlation, it is important to note down certain important artefacts 
that can then be used to connect the dots. These important artefacts can
 include IP addresses, machine names, user names, hashes, file paths, 
etc.

Correlation requires a lot of hypothesis creation and 
ensuring that the evidence supports that hypothesis. A hypothesis can be
 something like the user downloaded malware from a spoofed domain. The 
evidence to support this can be proxy logs that support the hypothesis 
that a website was visited, the website used a spoofed domain name, and a
 certain file was downloaded from that website. Now, let's say, we want 
to identify whether the malware executed through some vulnerability in 
an application or a user intentionally executed the malware. To see 
that, we might look at the parent process of the malware and the command
 line parameters used to execute the said malware. If the parent process
 is Windows Explorer, we can assume the user executed the malware 
intentionally (or they might have been tricked into executing it via 
social engineering), but if the parent process is a web browser or a 
word processor, we can assume that the malware was not intentionally 
executed, but it was executed because of a vulnerability in the said 
application.

!https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730369457912.png

## Is this a TP or an FP?

Similar to every SOC, the analysts in the Wareville SOC
 also need to differentiate TPs from FPs. This becomes especially 
difficult for them near Christmas when the analysts face alert fatigue. 
High chances of misclassification of TPs into FPs and vice versa are 
present in such times. The analysts, therefore, appreciate any help they
 could get from us in this crucial time. To make matters worse, the 
office of the Mayor has sent the analysts an alert informing them of 
multiple encoded powershell commands run on their systems. Perhaps we 
can help with that.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/57827a3b-6981-41ea-afa7-e36bb3e523e3/image.png)
![image](https://github.com/user-attachments/assets/95acaf7a-9f25-40dd-aada-1aadf055867e)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/5ef2ea3d-1ca4-4452-8249-4db5b69c7d70/image.png)
![image](https://github.com/user-attachments/assets/73ffd1a5-329c-4950-be0c-6c76974f0abc)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/a18429be-5f06-411d-8378-c6a553225968/image.png)
![image](https://github.com/user-attachments/assets/6c54e7ad-8c01-45b6-ac4a-4d91071a64de)

narrowing down categories
![image](https://github.com/user-attachments/assets/8c70c765-626e-4191-84e5-2d0e081dd74a)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/97d19115-29f7-4fcc-87b7-e098f1257999/image.png)

someone ran the same encoded PowerShell command on multiple machines. Another thing to note here is that before each execution of the PowerShell command, we see an authentication event, which was successful. 
![image](https://github.com/user-attachments/assets/86c9e1ad-2500-4a1e-986a-323e5a3e56da)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/aff882c0-30db-4a81-bf57-ee6653e15293/image.png)
![image](https://github.com/user-attachments/assets/ae237f92-e2ea-42c3-9d83-117d49077b05)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/035780aa-132a-4679-a823-d6db175a5040/image.png)
![image](https://github.com/user-attachments/assets/f952d4f2-4c45-476e-a327-7ceed4fb34c3)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/680fb26e-6c7d-4850-aa72-dc6a9e86333d/image.png)
![image](https://github.com/user-attachments/assets/fb32a374-fceb-4343-a436-18b6e09366f1)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/bd436a51-3cf4-4e69-8863-9b3ed3662734/image.png)

Our suspicions are rising. It seems that someone tried a brute-force attack on December 1st, as shown by the same filters applied above.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/6aa6bd31-04b8-4f3e-9567-ea3c577fc9e5/2c643104-a45c-497c-932a-f214c8259a5d/image.png)

The results also showed that they succeeded with the brute-force attempt because of the successful authentication attempt and quickly ran some PowerShell commands on the affected machines. Once the PowerShell commands were run, we didn't see any further login attempts.
