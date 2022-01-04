# Operationalizing Machine Learning
**An overview of the project**

The project is part of Udacity NanoDegree program and in this project we deploy ML models on Microsoft Azure to operationalize. AutoML is one feature we used in this project to train the model and pick the best classifier for deployment. We also use python sdk to interact with the Azure ML platform. The model is then consumed using a python script from the local windows machine using SDK. The scoring endpoint and auth key was nedded to do that. The output is shared below in the screen later shots. Finally we created a pipeline to automate the entire workflow using jupyter notebook as control place and using Azure ML SDK and libraries to interact with Microsoft Azure.

The setps are shown below in the image. 

![image](https://user-images.githubusercontent.com/19474037/147993721-d8a06993-99bc-4581-b79c-f2470db1c21e.png)


***SDK set up and Authentication***

Firstly Azure ML sdk is setup in the poweshell. **Note**: I used my own Azure subsription and created the preliminary steps for service principal and RBAC after az login. This gave the access to workspace (MLOPS) and resource group. 

***Upload Dataset***

Dataset file bankmarketing_train.csv was first uploaded and AzureML automatically identified and parsed and created a dataset.

***AutoML Model***

I used AzureML studio to create a compute cluster and then moved to AutoML to create an automl run. This automl run used the previously created dataset and is a classification model. Primary metrics used in Weighted AUC for accuracy. An experiment is created and the AutoML is run. After almost 1 hour the run got completed and the best model was displayed along with other metrics.

***Deploy Model***

The best model was deployed and an endpoint was created using AzureML studio (AMLS). The deployed model section is AMLS showd the swagger file, scoring URL and how to consume it (security key)


***Application Insight***

 Application insight was enabled by running the code and logging screenshots captured by running logs.py
 
 ***Swagger documentation***
 
 swagger json was downloaded from AzureML. Docker was installed and swagger.sh was run at port 9000 to view the swagger file. The file downloaded was served using a simple HTTPServer (serve.py) at port 8000. Once done swagger APP could show the AutoML deployed swagger file in rich UI.
 
 
 ***Consume endpoints***
 
 Modified the scoring_uro and key and executed the endpoint.py file. The data used for testing was downloaded from Sample data from AMLS. Got the optput printed as:
 {"result": ["no"]}
 
 ***create and publish pipeline using notebook***
 
 Using and modifying the notebook code (aml-pipelines-with-automated-machine-learning-step.ipynb). A new pipeline was created and published from AMLS (Notebook) using an conpute instance.
 
 
 
 

**An Architectural Diagram**

![image](https://user-images.githubusercontent.com/19474037/147995562-711df9ee-8b1b-4bd9-827f-76a86f0e521f.png)


***Detailed screenshots of the steps***

**Dataset**:

![image](https://user-images.githubusercontent.com/19474037/147996031-e354d0cb-1912-4c39-8ec0-c35cf2cca114.png)


**AutoML config***

![image](https://user-images.githubusercontent.com/19474037/147996168-fa5c2d3b-2a2b-497b-b375-adfcafe55c31.png)

![image](https://user-images.githubusercontent.com/19474037/147996225-408231ce-01a9-4288-9ed2-742678cfd30d.png)


***pipeline***

![image](https://user-images.githubusercontent.com/19474037/147996303-06d6d40c-af45-4db2-915f-106e818519d7.png)


![image](https://user-images.githubusercontent.com/19474037/147996334-1f6b05cd-d162-4349-a3d3-27dcc388bc1f.png)

![image](https://user-images.githubusercontent.com/19474037/147996413-35223bba-e30c-4b79-b090-e83853fdedda.png)

![image](https://user-images.githubusercontent.com/19474037/147996450-e1674061-80bc-4976-8a8b-0d875fd10820.png)

![image](https://user-images.githubusercontent.com/19474037/147996483-b3ae69a4-fcc8-453a-99aa-cdf8a8eea07f.png)

![image](https://user-images.githubusercontent.com/19474037/147996509-98d67172-c597-4b99-a9c5-9aa98b330eb4.png)

![image](https://user-images.githubusercontent.com/19474037/147996637-6d569d08-62fc-435a-acff-50595e85271d.png)

![image](https://user-images.githubusercontent.com/19474037/147996651-60372bd3-47da-41ed-bf2b-4a86864a9638.png)

![image](https://user-images.githubusercontent.com/19474037/147996662-b015de6c-506a-4f37-b3cc-2dba00b78186.png)

![image](https://user-images.githubusercontent.com/19474037/147996667-636d48fa-1a65-4fa8-83e9-a763f68c0825.png)

![image](https://user-images.githubusercontent.com/19474037/147996680-31b12fdd-0b49-4bcc-b870-73304e2615b3.png)

**AutoML Run from AMLS and consuming endpoint**
***Step 1: Creating Service Principal & Authentication***

Create service principal account and associate it with my specific workspace:

![image](https://user-images.githubusercontent.com/19474037/148012188-bb63cd4f-71ee-49e0-9490-16668bfde071.png)


![image](https://user-images.githubusercontent.com/19474037/147996873-036a79c8-6b0e-466c-b2f9-bcca8c11c937.png)

![image](https://user-images.githubusercontent.com/19474037/147997045-b672c412-881e-448f-8120-b45c8cbb2f65.png)

![image](https://user-images.githubusercontent.com/19474037/147997061-85e8eacc-8fe5-42a0-b10f-bca5ade517b6.png)

![image](https://user-images.githubusercontent.com/19474037/147997067-45451d10-5493-42ba-ac4a-233b7b93ece7.png)

![image](https://user-images.githubusercontent.com/19474037/147997256-9721443e-f29d-4e54-a81f-9bb95ba90971.png)


![image](https://user-images.githubusercontent.com/19474037/147997112-97c5db42-01b9-4b38-95bb-f34b819af2ad.png)

![image](https://user-images.githubusercontent.com/19474037/147997151-f741a8c1-7c89-4c7b-b1bb-ea5dd676f55f.png)

![image](https://user-images.githubusercontent.com/19474037/147997327-73ddb37f-5a78-4fd5-ba87-4371f3e1963f.png)





**A short description of how to improve the project in the future**

1. The pipeline can be triggered on a scheduled basis as of when we get new dataset. This will ensure model is not drifting
2. Create alerts when model accuracy degrades so that ML engineers can look at it and if needed redeploy the model using feature engineering and retraining.
3. create seperate pipelines for each ML steps and then combine it using a pipeline. This will ensure that data engineers, ML engineers, AI scientist, Operation can work parallely.


***screencast***

https://www.youtube.com/watch?v=kSjAJpjyvJw





