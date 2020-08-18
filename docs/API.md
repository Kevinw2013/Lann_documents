# Model deployment

> Installation instruction

Firstly, please make sure docker is installed in your environment. Next, after downloading the docker image file of your model (e.g., test.tar) please complete the following.

1. docker load -i /your image path/test.tar

2. docker run -d --network host --name mytest run “pip:test”

> Notes:

1. The default tag of your docker image is the name of downloaded tar file. In the above example, the tag of test.tar is pip:test.

2. The parameters of running docker should be adjusted according to your network.

3. The default port of docker is 8080. Use server.port to customize it, e.g. docker run -d --network run “pip:test” --server.port 9999

Once the model is initiated, simply call the API with two parameters: id of the model and text to be processed:

{"pipelineId":"test","text":"hi,i am  diabetes and cancer patients"}

curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"pipelineId":"test","text":"hi,i am  diabetes and cancer patients"}' 'http://127.0.0.1:8080/query/brat'

{

  "docentiry": [
    {
      "id": 0,
      "docId": "xx",
      "startPos": 9,
      "endPos": 17,
      "semType": "clinical_finding",
      "seert": null,
      "entText": "diabetes",
      "code": null,
      "attr1": null,
      "attr2": "",
      "attr3": "",
      "attr4": ""
    },

    {
      "id": 0,
      "docId": "xx",
      "startPos": 22,
      "endPos": 37,
      "semType": "clinical_finding",
      "seert": null,
      "entText": "cancer patients",
      "code": null,
      "attr1": null,
      "attr2": "",
      "attr3": "",
      "attr4": ""
    }
  ],

  "bratFile": "{\"text\":\"hi,i am  diabetes and cancer patients\",\"entities\":[[\"T0\",\"clinical_finding\",[[9,17]]],[\"T1\",\"clinical_finding\",[[22,37]]]],\"relations\":[]}",
  "bratSem": "{\"entity_types\":[{\"type\":\"clinical_finding\",\"labels\":[\"clinical_finding\"],\"bgColor\":\"#00FF00\",\"borderColor\":\"darken\"}],\"entity_attribute_types\":[],\"relation_types\":[],\"event_types\":[]}"

}

###

