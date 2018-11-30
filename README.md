# OpenSource India

## Blockchain Workshop

Hyperledger Fabric using IBM Container Service

Following are the steps to be followed:

## 1. Register on IBM Cloud

http://bit.ly/ibmcloudsignup

Convert the IBM Cloud Lite account to Trial account
Account -- Billing and Usage -- Apply Promo Code

Please follow the pdf - [IBM Cloud Sign up and PROMO Code](https://github.com/IBMDevConnect/OSIBlockchainWorkshop/blob/master/IBM%20Cloud%20Sign%20up%20and%20PROMO%20Code.pdf)

## 2. Create a Kubernetes cluster on IBM Cloud
Sign in using IBMCloud ID. GoTo "Catalog" and search for "Kubernetes". In the search result you should see the "Kubernetes Service". Click on the "Kubernetes Service" to create the Kubernetes service on IBM Cloud. 

## 3. Visit the code pattern at the following link:

[Deploy Hyperledger Fabric network on IBM Cloud](https://developer.ibm.com/patterns/deploy-hyperledger-fabric-network-on-ibm-cloud)

## Query 

Chaincode was instantiated with the values as { a: 100, b: 200 }. Let’s query to org1peer1 for the value of a to make sure the chaincode was properly instantiated

``` 
peer chaincode query -C channel1 -n cc -c '{"Args":["query","a"]}'

```

Similarly for be
``` 
peer chaincode query -C channel1 -n cc -c '{"Args":["query","b"]}'

```



## Invoke chaincode which makes payment of X units from A to B

Now let’s submit a request to org2peer1 to move 20 from a to b. A new transaction will be generated and upon successful completion of transaction, state will get updated

```
peer chaincode invoke -o blockchain-orderer:31010 -C channel1 -n cc -c '{"Args":["invoke","a","b","20"]}'

```
## Query

Let’s confirm that our previous invocation executed properly. We initialized the key a with a value of 100 and just removed 20 with our previous invocation. Therefore, a query against a should show 80 and a query against b should show 220. Now issue the query request to org3peer1 and org4peer1 as shown

```
kubectl exec -it <<pod name>> bash
  
peer chaincode query -C channel1 -n cc -c '{"Args":["query","a"]}'

peer chaincode query -C channel1 -n cc -c '{"Args":["query","b"]}'

```
