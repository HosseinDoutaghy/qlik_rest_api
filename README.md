Designing a messaging web service
------

I have decided to include the name of the application and the version of the API in the URL to separates this service from others that can be running on the same system. The API version is also included in the URL that can help with making updates in the future without affecting applications that rely on the older functions. 

Here are the API end-points:

- GET			
    - http://[IP]/v1/mma/messages/all		
    - Retrieve list of messages
    - Example: http://127.0.0.1:5000/v1/mma/messages/all

- GET			
    - http://[IP]/v1/mma/messages			
    - Retrieve a message
    - Example: http://127.0.0.1:5000/v1/mma/messages?id=1

- POST		    
    - http://[IP]/v1/mma/messages			
    - Create a new message
    - Example: curl -i -H "Content-Type: application/json" -X POST -d '{"message": "hello Moe"}' http://127.0.0.1:5000/v1/mma/messages

- PUT			
    - http://[IP]/v1/mma/messages			
    - Update and existing message		
    - Example: curl -i -H "Content-Type: application/json" -X PUT -d '{"message": "hello Moe", "id": 1}' http://127.0.0.1:5000/v1/mma/messages
    
- DELETE		
    - http://[IP]/v1/mma/messages			
    - Delete a message
    - Example: curl -i -H "Content-Type: application/json" -X DELETE -d '{"id": 1}' http://127.0.0.1:5000/v1/mma/messages

Parameter: 
- id: 			unique identifier for messages. Numeric type.
- message: 		message description. Text type.
- palindrome: 	TRUE/FALSE.

Our application was written in python and Flask web framework was used to create the REST API services. The application has been dockerized and can be installed by runnig the install.sh script.

*Installation*
----

To install the app, unzip the package and go to root directory of the package and run 'sudo ./install.sh'. Before that make sure Docker is installed in your environment. The install script will build a docker image and then run a container that our application will use to run. Once you see this message 'Successfully built <container_ID>' in the terminal, run 'sudo docker pa -a' to make sure the container is running and then check the logs to confirm the app has started and ready 'sudo docker logs mma-app'. 

*Testing*
----

If you have curl installed in your environment, you could run the api_test.sh script to test the API. 

*Kubernetes*
----

There is kubernetes deployment yaml file in the package which was not fully tested for this application.. The docker image should exist in the local repo on the host in which you are running the deployment from as well as on the node in which the pods will run on. This was not an issue if the docker image was available in a repo where the deployment could access and downaload it. 

To deploy using kubectl:
- sudo kubectl apply -f deployment.yml

To check the pods status:
- sudo kubectl get all

To find out more about the status of the pods:
- sudo kubectl describe pod <POD_NAME>
