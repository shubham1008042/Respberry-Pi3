                                    Connect Device To AWS IoT Core

Step 1: Register your device in the registry:

1.On the Welcome to the AWS IoT Console page, in the navigation pane, choose Manage.

2.On the You don't have any things yet page, choose Register a thing. 

3.On the Creating AWS IoT things page, choose Create a single thing. 

4.On the Create a thing page, in the Name field, type a name for your thing, such as  MyIotThing. Choose Next

5.On the Add a certificate for your thing page, choose Create certificate. This generates an X.509 certificate and key pair. 

6.On the Certificate created! page, download your public and private keys, certificate, and root certificate authority (CA): 
1. Choose Download for your certificate. 
2. Choose Download for your private key. 
3. Choose Download for the Amazon root CA. This will display a new web page. 

7.On the Add a policy for your thing page, choose Register Thing. 

8.On the AWS IoT console, in the navigation pane, choose Secure and Policies. Choose Create. 

9.On the Create a policy page: 
1. Enter a Name for the policy, such as MyIotPolicy. 
2. For Action, enter iot:*. For Resource ARN, enter *. 
3. Under Effect, choose Allow, and then choose Create. 

10.Choose Manage and then choose your AWS IoT thing. 

11.Choose Security

12.Choose your certificate.

13.In the certificate detail page, choose Actions and then Attach policy.

14.Choose the policy you created (MyIotPolicy) and choose Attach.


Step 2: Create and Activate a Device Certificate:

1.Choose Create certificate. 

2.On the Certificate created! page, choose Download for the certificate, private key, and the root CA for AWS IoT (the public key need not be downloaded). Save each of them to your computer, and then choose Activate to continue. 

3.Choose Done to return to the AWS IoT console main page. 

Step 3: Create an AWS IoT Policy:

1.In the left navigation pane, choose Secure, and then Policies. On the You don't have a policy yet page, choose Create a policy. 

2.On the Create a policy page, in the Name field, type a name for the policy (for example, MyIotPolicy). 

3.After you have entered the information for your policy, choose Create. 


Step 4: Attach an AWS IoT Policy to a Device Certificate :

1.In the left navigation pane, choose Secure, and then Certificates. 

2.In the box for the certificate you created, choose ... to open a drop-down menu, and then choose Attach policy. 

3.In the Attach policies to certificate(s) dialog box, select the check box next to the policy you created in the previous step, and then choose Attach. 

Step 5: Attach a Certificate to a Thing:

1.In the box for the certificate you created, choose ... to open a drop-down menu, and then choose Attach thing. 

2.In the Attach things to certificate(s) dialog box, select the check box next to the thing you registered, and then choose Attach. 

3.To verify the thing is attached, select the box representing the certificate. 

4.On the Details page for the certificate, in the left navigation pane, choose Things. 

5.To verify the policy is attached, on the Details page for the certificate, in the left navigation pane, choose Policies. 

Step 6: Configure Your Device:

All devices must have a device certificate, private key, and root CA certificate installed in order to communicate with AWS IoT. Consult your device's documentation to connect to it and copy your device certificate, private key, and root CA certificate onto your device. 

Step 7: View Device MQTT Messages with the AWS IoT MQTT Client :

1.In the AWS IoT console, in the left navigation pane, choose Test. 

2.Subscribe to the topic on which your IoT thing publishes. Continuing with this example, in Subscribe to a topic, in the Subscription topic field, type my/topic, and then choose Subscribe to topic. 

Choosing Subscribe to topic above, results in the topic my/topic appearing in the Subscriptions column. 

Choose Publish to topic. You should see the message in the AWS IoT MQTT client (choose my/topic in the Subscription column to see the message). 

Step 8: Configure and Test Rules:

a) Create an SNS Topic:
Use the Amazon SNS console to create an Amazon SNS topic.

Note:
Amazon SNS is not available in all AWS regions. 

1. Open the Amazon SNS console. 

2. On the left pane, choose Topics. 
      a)Choose Create new topic. 
      b)Type a topic name and a display name, and then choose Create topic. 
      c)Make a note of the ARN for the topic you just created.
       
b) Subscribe to an Amazon SNS Topic :

To receive SMS messages on your cell phone, subscribe to the Amazon SNS topic.
1. In the Amazon SNS console, select the check box next to the topic you just created. From the Actions menu, choose Subscribe to topic. 

2. On Create subscription, from the Protocol drop-down list, choose SMS. 
In the Endpoint field, type the phone number of an SMS-enabled cell phone, and then choose Create subscription. 

c) Create a Rule:

1. In the AWS IoT console, in the left navigation pane, choose Act. 

2. On the Act page, choose Create a rule. 

3. On the Create a rule page, in the Name field, type a name for your rule. 

4. Scroll down to Rule query statement. Choose the latest version from the Using SQL version drop-down list. In the Rule query statement field, type SELECT * FROM 'my/topic'. 

5. In Set one or more actions, choose Add action. 

6. On the Select an action page, select Send a message as an SNS push notification, and then choose Configure action. 

7. On the Configure action page, under SNS target, choose Select to expand the SNS topic drop down. Then choose Select next to the Amazon SNS topic you created earlier. Under Message format select JSON. 

8. Now give AWS IoT permission to publish to the Amazon SNS topic on your behalf when the rule is triggered. Choose Create a new role. Enter a name for your new role in the IAM role name field. After you have entered the name, choose Create a new role. 

9. Under IAM role name, choose Update role to apply the permissions to the newly created role, choose the newly created role, and choose Add action. 

10. On the Create a Rule page, choose Create rule. 

Step 9: Test the Amazon SNS Rule:

1. In the AWS IoT console, in the left navigation pane, choose Test. 

2. On the MQTT client page, in the Publish section, in the Specify a topic and a message to publish… field, type my/topic or the topic you used in the rule. In the message payload section, type the following JSON: 

3. Choose Publish to topic. You should receive an Amazon SNS message on your cell phone. 
