##Rag Based solution:<br/>
###Steps:<br/>
In order to create a knowledge base we need to login as IAM user.<br/>
1.Create an s3 bucket<br/>
2.Upload the required documents into the s3 bucket<br/>
3. Go to amazon bedrock and make sure you are in region us-east-1 <br/>
4. Go to knowledge base tab-> create a knowledge base<br/>
5. In the knowledge base add the s3 bucket in which we uploaded documents, next select a default chunking and select the amazon titan v2 embedding model and lastly select opensearch documents vector store-> click on create.<br/>
6.now sync the database to prepare and get ready to use the opensearch vector store. <br/>
7. Create a lambda function<br/>
8. After creating a lambda function we need to set two environment variables in config which are knowledge base id and foundation model arn.<br/>
9.we will be using retrieve and generate api in lambda functionto retrieve the data and generate the response<br/>
(https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/bedrock-agent-runtime/client/retrieve_and_generate.html)<br/>
10.also we need to change the time out time to one min or more since default timeout is set to 3 sec which is not sufficient to perform the lambda function.<br/>
11.now in order to access the bedrock lambda function need permission so we have to give awsbedrockfullaccess permission to the lambda role. <br/>
12. Now we can test the lambda function using the test by giving a name and giving the question in json format.<br/>
13. We have to create the rest api gateway by attaching the lambda function which is created and using the post method. <br/>
14. Now we can test it by giving the query in the request body and it will work fine. <br/>
15. Now, deploy the api to a new stage. Once its been deployed we can copy the invoke url.<br/>
16.now try to invoke this by using postman. I.e paste the url in postman to invoke the bedrock from the api from stages and send the request through postman and access the model.
17.now we can create a web page to ask the question and the bot will answer the question using the knowledge base and bedrock model .<br/>
18. In order to create this website we are using a streamlit app library in python and using visual studio code we will run the website and invoke the bedrock using the same api which we used in postman. <br/>
19. We need to run the command called streamlit run app.py. Then we see the website opened in the designated port .
