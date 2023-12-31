# How to Use
## MQSubscriber class

```java
//new object need to set all the required information
MQSubscriber subscriber = new MQSubscriber(broker,username,password,clientid,subscribeTopic,qos);

//set callback function when receive message from the subscribeTopic
subscriber.setCallback(new MQSubscriberCallbackInterface() {
            @Override
            public void messageHandler(String topic,JSONObject msg) {
                // Code for handling the subscribed message
                System.out.println("msg: "+ msg);
            }
        });

//Start listening the subscribeTopic
subscriber.startListening();

//Actively request for the publisher to get the new information
JSONParser parser = new JSONParser();
JSONObject msg  = (JSONObject) parser.parse("{\"msg\":\"request device info\"}");
JSONObject result = subscriber.getDeviceInfo(getDeviceInfoTopic,msg);
System.out.println(result);

//Using this client to send message
subscriber.sendMsg(topic,msg);
```

## MQSubscriberCallbackInterface interface

For setting the callback function when receive message from the subscribeTopic.

```java
new MQSubscriberCallbackInterface() {
            @Override
            public void messageHandler(String topic,JSONObject msg) {
              	//code for handling the new message
                System.out.println("msg: "+ msg);
            }
        }
```

### Try to run using the test class MQSubscriberTest.java
