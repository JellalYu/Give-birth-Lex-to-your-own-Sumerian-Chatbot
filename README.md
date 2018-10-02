## Scenario
Amazon Sumerian is an AWS service for creating 3D applications that support AR and VR services. It can be applied to the product presentation in various scenarios. You can also build a chatbot in Amazon Sumerian. 
Based on the [**previous Lab**](https://github.com/ecloudvalley/Create-a-Comprehend-Translate-Chatbot-in-Lex), this Lab combined amazon Sumerian and Polly to create a more interactive chatbot.

![1-2.png](/Imgs/1-2.png) 


## Prerequisites
1. The workshop’s region will be in **US east (N.Virginia)**.
2. Build a Lex Chatbot follow [**Create a Comprehend & Translate Chatbot in Lex**](https://github.com/JellalYu/Create-a-Comprehend-Translate-Chatbot-in-Lex).
3. Create an [**Amazon Cognito Identity Pool ID**](https://docs.aws.amazon.com/cognito/latest/developerguide/tutorial-create-identity-pool.html).


## Lab tutorial

### Create a Cognito identity pool ID
Before we get to editing a scene in Sumerian, we need to set up an AWS CloudFormation stack.

1.    Sign in to Amazon with your AWS account and open **Cognito**.
2.    Type **Manage identity Pools**.
3.    In Federated identities page, click **Create new identity Pool**.
4.    In Getting started wizard page, enter your own identity pool name and check the **Enable access to unauthenticated identities** box.

![2.PNG](/Imgs/2.PNG) 

5.    Then **Create Pool**.
6. Go to your Identity and copy identity pool ID to your text editor.

![3.PNG](/Imgs/3.PNG)

---
### Build Sumerian scene
1. Open **Sumerian** in AWS console.
2. In Create scene from template, choose **Default Lighting** and make the name as **MySumerian**.

![4.PNG](/Imgs/4.PNG)

3. In edit page, type **Import Assets** and choose Sumerian 3D models you like. 

![5.PNG](/Imgs/5.PNG)

4. Drag the **model entities** in Assets to Editor Cam.

![6.PNG](/Imgs/6.PNG)

5. Paste the Cognito Identity Pool ID you just created. 

![7.PNG](/Imgs/7.PNG)

6. Click your bot model and type **Add Component** below and add **Dialogue**. 

![8.PNG](/Imgs/8.PNG)

7. Check your Chatbot in Lex has an **Alias name** and **Publish**. 

![9.PNG](/Imgs/9.PNG)

 8. Edit Dialogue name and alias as your Lex setting.
 
![10.PNG](/Imgs/10.PNG)

---
### Add State machine
Here, we will establish the Sumerian Chatbot behavior flow through the state machine, and it will take actions according to this setting.

1. Add **State machine**.

![11.PNG](/Imgs/11.PNG)

2. Rename the behavior name to "Chatbot_beh".

3. Rename State 1 to "Start".

![12.PNG](/Imgs/12.PNG)

4. Choose **Add Action**, and then search for and add the **AWS SDK Ready** action.

![13.PNG](/Imgs/13.PNG)

5. Add **Wait for Input** State:

![14.PNG](/Imgs/14.PNG)

* Rename the state to "Wait for Input".
* Add the Key Down action.
* Click inside the Key property text box and press the spacebar. This sets the Key Down key action to the spacebar.

![15-2.PNG](/Imgs/15-2.PNG)

6. Add **Wait for input** State.

![16-3.PNG](/Imgs/16-3.PNG)

7. Add **Get text input** State.

![17-2.PNG](/Imgs/17-2.PNG)

8. Add **Process with Lex** State.

![18.PNG](/Imgs/18.PNG)

9. Add **Play Response** State.

![19.PNG](/Imgs/19.PNG)

10. Add **Adding Transitions** State.

![20.PNG](/Imgs/20.PNG)

11. Set the **Start** and state to **Set As Initial State**.

![21.PNG](/Imgs/21.PNG)

12. The final graph will look like the following.

![22.PNG](/Imgs/22.PNG)


13. Create a TextBot Behavior for Text Input:
*  **Create Entity** and choose **</>**.

![23.PNG](/Imgs/23.PNG)


*  With the HTML entity selected, expand the **HTML** component, and then choose **Open in Editor**.

![24.PNG](/Imgs/24.PNG)

* Paste the following code:

```
<style>
     /*
      * Place your styles here. Beware that CSS styles affect all
      * HTML elements in the page, so you need to provide appropriate
      * classes or IDs to identify the element being styled.
      */

     #lexInput {
         background: #fefefe;
         font-size: 16px;
         padding: 10px;
         border-radius: 3px;
         margin: 0;
         font-family: sans-serif;
         width: 250px;
     }
 </style>

 <input type="text" id="lexInput"/>
```
---
### Test the Chatbot
Now you can test your chatbot by text, Try to say hi to your Sumerian.

![25.PNG](/Imgs/25.PNG)

---
## Conclusion
* Congratulations! Now you can make a simple Sumerian chatbot with Amazon Lex. 

