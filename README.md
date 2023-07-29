# Build, train, and deploy a fraud detection model with Amazon Fraud Detector

**<h3> What is Amazon Fraud Detector? </h3>**
Amazon Fraud Detector is a fully managed service that is used to identify potentially fraudulent online payment fraud and the creation of fake accounts. It works by using a smart system that learns from past experiences and data. This system can spot patterns and signals that may indicate fraudulent or deceptive activities. For example, it can recognize if someone is trying to use a stolen credit card, fake credentials, or any other sneaky tactic.

Amazon Fraud Detector helps Amazon and its customers by identifying potential fraud before it causes harm. By doing this, it helps keep everyone's online transactions safer and more secure.

**<h3> Overview </h3>**
Step 1: Amazon fraud detector components.<br>
Step 2: Create the bucket for the training data.<br>
Step 3: Create an event for the fraud detector model.<br>
Step 4: Tain and deploy the fraud detection model.<br>
Step 5: Create and publish the fraud detector.<br>
Step 6: Create detectors.

**<h3> Step 1: Amazon fraud detector components. </h3>**
**Detector:** A detector is a configured entity that represents the fraud detection logic. It is a higher-level concept that brings together various components to detect fraudulent behavior. A detector consists of rules, which are conditions or criteria that the system uses to evaluate incoming data. These rules can be simple or complex, depending on the specific fraud scenarios that the detector aims to detect.

**Models:** The model, in Amazon Fraud Detector, is a machine learning model that learns from historical data containing both legitimate and fraudulent examples. This model is the core component that evaluates the data and makes predictions based on patterns and signals it has learned during the training phase. The training data is used to teach the model what legitimate and fraudulent behavior looks like, so it can differentiate between them when presented with new, unseen data.

To create models, we must provide data for training. This data includes variables and labels. Additionally, we can also define events based on the entities sending the data for prediction.

**<h3> Step 2: Create the bucket for the training data. </h3>**
Note: First, download and save the dataset. Then, extract the files using an archive utility. Download here: [training_data.zip](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/files/12206320/training_data.zip)
1. Go to Amazon S3.
2. Create a new bucket. Name the bucket **fraud-detector-bucket1** and choose **us-east-1** as the region. Leave the default settings and create bucket.
3. Select the bucket, open it, and add new files as an object. Note: We will upload the **registration_data_20K_minimum.csv** file.
4. Done

![1](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/f86b7da4-0086-46ea-9d7a-8ea2a3d3f077)

![2](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/96bda2f8-71ae-4cc2-a2a0-6e2eec29fce0)

![3](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/ddbe612e-5857-47bd-a769-40c7c7803d69)

![4](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/3fb78ac2-ec10-4d8a-a682-0a842251b5bb)

![5](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/6867a8c5-72e2-424e-8155-9045cf36e753)

![6](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/344a72bf-49c3-4178-9b3f-8fa39da4a69a)

**<h3> Step 3: Create an event for the fraud detector model. </h3>**
To create an event, you first define the entities participating in the event, then define the labels and variables in the event data.

1. **Create Entity.**

   **Entity:** An entity represents who is performing the action.
   1. Go to Fraud Detector Console.
   2. On the left navigation pane, click open **Entities**.
   3. Click open **Create Entity.**
   4. Put Entity name as **customer**.
      
![7](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/ceb18700-72df-4fc7-b4cb-b3438a347dca)

![8](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/3324ba43-e446-486f-87ac-9e270f5a28f4)

![9](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/d03b2331-2458-40ba-8538-b04acfe4ceb8)

![10](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/53b9587e-d951-42fd-b36e-ab4687c458f1)

2. **Create two labels.**
   
   **Label:** A label classifies an event as **Fraud** or **Legit**.
   1. Go to Fraud Detector Console.
   2. On the left navigation pane, click open **Labels**.
   3. Click on **Create label**
   4. Create two labels **(1) Fraud (2) Legit.**

   ![11](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/4d2e1ec7-913e-442e-b794-0f693e43d6b4)

![12](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/362bd446-ec0c-4c89-bdd7-f5cd9360fde3)

![13](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/d64ce2af-ce56-4d9b-9112-5dc7b265d991)

![14](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/bf3c7592-bab3-490d-b1a3-6f8d6a486967)

![15](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/34c956f7-4360-41d3-82e8-60d4aff08e91)

3. **Create an Event.**
 
   **Event:**  An event type defines the structure for an event sent to Amazon Fraud Detector. This includes the variables sent as part of the event, the entity performing the event (such as a customer), and the labels that classify the event.
   1. Go to Fraud Detector Console.
   2. On the left navigation pane, click open **Events**.
   3. Click on **Create Event type**.
   4. For Name, type **registration**.
   5. For entity, choose the **customer** entity.

![16](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/00a4f8ce-c2a3-473f-9f4d-6d41124b165e)

![17](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/efffbc7d-c1e0-401a-8a72-26eab5091017)

![18](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/21f2919e-1723-49e1-856e-63d2ca29665d)

   6. In the **Event variables** box, make the following selections:
      
![19](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/61461a23-eacc-4b91-ab56-6d45c7e0f516)

![20](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/7795867f-7ad7-4b99-a0bf-fe48134e605f)

![21](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/8e762812-266d-4469-81ea-5774d99590de)

![22](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/9e1baf04-0d87-4b26-8969-2a45dd7bc4ef)

The details for your newly created registration event appear with the associated variables and labels.

![23](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/48d8cd81-fd4e-47b6-a8ad-74f03dd05306)

**<h3> Step 4: Train and deploy the fraud detection model. </h3>**

1. Go to Fraud Detector Console.
2. In the left navigation pane choose **Models**.
3. Then, choose Add model, Create model.

![24](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/6aee210e-2629-476a-84a7-9a79abc6ae23)

4. For the Model name, put **fraud_detection_model** and configure like I did.

![25](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/d7e3b4d4-fc3a-49b7-8b19-90981c806857)

5. Historical event data.

![26](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/29b8ef98-4143-40df-ab6d-965064f7a238)

6. Configure training.

![27](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/3402a6c6-5435-49c3-a4c2-24f7e097a98e)

![28](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/1e8d69a8-5b2e-47bb-aa03-24dde9fceb05)

7. On the **Review and Create page**, review all the information and choose** Create and Train model**.

![29](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/d3100ac4-6881-43ff-9427-a165ad64791e)

This process takes around 40 minutes. So, wait.

8. Check the status and you will see its status is **Training**.

![30](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/9df6db7d-d96b-4007-9b21-41500ce69d81)

9. When the model is ready, the Status changes from **Training** to **Ready to Deploy**.

![31](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/560d2d7e-2ee0-472c-9ed3-4f612119dca3)

10. When the Model version status is **Ready to Deploy**, under Version, **choose 1.0**. The Version details view opens.
11. Select the Version details page and choose **Actions**, **Deploy model version**, and then choose **Deploy version**.

![32](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/33028015-95c4-4b41-b4d8-7f474a52c9dd)

![33](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/73efd8de-692e-4be2-bc62-c072c9b11960)

12. When the model is ready, the Status changes to **Active**.

![34](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/71141d33-4b55-40d9-8667-c97156eba65a)

**<h3> Step 5: Create and publish the fraud detector. </h3>**

 After you create the fraud detector, you test the outcomes with sample training data, then finally publish the detector.

1. Go to Fraud Detector Console.
2. In the left navigation pane choose **Outcomes**.
3. Create three outcomes by the name of **high_risk**, **medium_risk**, and **low_risk**.

![35](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/8ea17922-661c-4314-8753-c51f772f414f)

![36](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/dbfafa85-0193-4893-971a-10700100b38c)

![37](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/1d20cccd-6184-4a6e-9eff-4da611d2727e)

![38](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/66dea5a1-21bc-426a-88cc-6eba0eecff08)

4. Once done creating outcomes, your list of **Outcomes** now includes three outcomes.

![39](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/e0fddcac-93be-4756-8b5e-5f9418af0303)

**<h3> Step 6: Create detectors. </h3>**

Detectors are comprised of models and rules that evaluate events for fraud.
1. Go to Fraud Detector Console.
2. In the left navigation pane choose **Detectors**.
3. Create **detector.**

![40](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/ea6c3f51-33d8-4e9a-a521-5b10eff0bd7b)

4. For the Detector name, type **my-detector.**
5. For Event type, choose **registration**. Then, choose **Next**.

![41](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/11348321-df42-450a-85a5-357a5f050ab5)

6. On the **Add model page**, choose **Add model**.

![42](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/03db06cb-77dd-4fdc-adbb-44d0e9e31ccf)

7. Add the model and select the version.

![43](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/fdedc3ae-7373-46ff-8477-6a4bc818b5c6)

8. Select the model and click **Next.**

![44](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/6e000666-2726-4e04-a02f-8c1cec1784e1)

9. On the **Add rules** page, create the three rules by the name of **auto-fraud-rule**, **review-rule**, and **auto-legit-rule**.
10. Configure the same.

![45](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/e7c1adcc-9ab2-4116-bdd6-709129dd7ee1)

![46](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/c7a1f6f1-72e7-4969-b224-605082896e91)

11. Configure rule execution.

![47](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/2d52af3e-2737-4a0f-9765-5f4a08c8e93c)

12. Review and create.

![48](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/457d027e-d3a2-47c6-9804-25bba26bd774)

13. On the detector details page, scroll down to the **Run test** section and enter the data from this row. Choose **Run test**. Paste the details from the **registration_data_20K_minimum.csv**.

![49](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/e1663709-46f9-49d1-a741-92cac6162384)

![50](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/616f9fbf-a4c7-4a4b-8db5-70f2477c3cae)

14. After you run the few sample test. Click on **Actions** and then choose **Publish**.

![51](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/40444cbf-ce34-4d6c-83a0-bbf295954a1a)

15. Once done, check the status and you will find it **Active**.

![52](https://github.com/ravinder-panwar/Build-train-and-deploy-a-fraud-detection-model-with-Amazon-Fraud-Detector/assets/133412857/d27dfeaa-7f8d-4f1f-9b57-88c0f2f0e710)

<h2> Congratulations! Project Completed. </h2>






































