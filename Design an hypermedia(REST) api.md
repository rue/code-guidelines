# How to design an hypermedia(REST) api
  
* [Introduction](#intro)
* [Available REST documentations](#doc)
* [Theory](#theory)
	* [Resources](#ressources)
	* [Addressability](#address)
	* [Representations](#representations)
	* [Uniformity of the interface](#uniformity)
	* [Connectivity](#connectivity)
	* [Statelessness](#stateless)
* [The real world and what we will focus on for now](#real-world)
* [Where can you find real world examples](#examples)

## <a name="intro"/>Introduction</a>
	
This guide should describe most of what REST is and its purpose. This is by no means an authoritative source and will be subject to change during time.
REST aims at making the machines be able to talk to each other without the need of human (coder) intervention. It standardizes the interactions between them.
With rpc you need to know in advance all the method with their parameters and return types for the client to be able to talk to the server.
The communication is so different from service to service that a programmer has to code the interaction between it's client and every services.
	
## <a name="doc"/>Available REST documentations</a>
	
* [http://tomayko.com/writings/rest-to-my-wife](http://tomayko.com/writings/rest-to-my-wife)
* Restful web services (available in pdf for free)

## <a name="theory"/>Theory</a>
	
### <a name="resources"/>Resources</a>
		
REST is all about resources. Everything in your service, from data access to computation, can be described as a resource. 
It is really important to grasp that concept, because by applying it you will always be able to use the corresponding VERBS for the CRUD of your resource.
When you are about to invent a custom VERB on your service, it means that you are missing a resource.
	
For example, lets say you have a method on your service that is called Buy: 
	
You would want to create a method thta make a customer buy a group of item, but here is no BUY verb defined in HTTP.
Instead, you would need a new resource called purchase and you would POST on /customer/123/purchases to create a new purchase for that customer. 
		
### <a name="address"/>Addressability</a>
	
Every resource has it's unique corresponding URI. eg. /items/5
It is really important that anybody who can access the resource does it with the same URI.

### <a name="representations"/>Representations</a>
	
A resource can be represented in different ways.
A client can ask for a representation in json, xml, raw representation (stream of the image) or anything that the server can support.
The accept http header is a perfect tool to describe to the server the format exptected by the client.
	
### <a name="uniformity"/>Uniformity of the interface</a>
	
This is what makes REST so different from xml rpc. The VERBS are already defined, no need to invent new custom verbs.
		
- GET on /resources to list the ressources
- GET on /resources/123 to read the resource
- HEAD on /resources/123 to check for the resource existence

- POST on /recources to create a new one (the server returns the created URL in the location header)
- PUT on /resources/123 to modify an existing one.
- DELETE on /resources/123 de delete it.
		
### <a name="connectivity"/>Connectivity</a>
	
### <a name="stateless"/>Statelessness</a>
	
## <a name="real-world"/>The real world and what we will focus on for now</a>

## <a name="examples"/>Where can you find examples</a>