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

The best example of REST one can give is web servers and browsers. The server gives all the info needed by the client to render its pages and access its resources.
The client has nothing hardcoded that tells him hwo to communicate to the server. But still, the is able to communicate with the server perfectly.

A part of this guide will be focused on describing what part the company will implement and what part will be kept on the ice for now.
Its purpose is to give you a good idea on how to maintain and build our web services.
	
## <a name="doc"/>Available REST documentations</a>
	
* [How I Explained REST to My Wife](http://tomayko.com/writings/rest-to-my-wife)
* Restful web services (available in pdf for free)

## <a name="theory"/>Theory</a>

### <a name="resources"/>Resources</a>
		
REST is all about resources. Everything in your service, from data access to computation, can be described as a resource. 
It is really important to grasp that concept, because by applying it you will always be able to use the corresponding VERBS for the CRUD of your resource.
When you are about to invent a custom VERB on your service, it means that you are missing a resource.
	
For example, lets say you have a method on your service that is called Buy: 
	
You would want to create a method that makes a customer buy a collection of items, but here is no BUY verb defined in HTTP.
Instead, you would need a new resource called purchase and you would POST on /customer/123/purchases to create a new purchase for that customer. 
		
### <a name="address"/>Addressability</a>
	
Every resource is identified by one or more URIs. A URI must always identify the same resource.
There is often a convention used where each resource only has a single unique URI, and that URI is used for all access to the resource.

### <a name="representations"/>Representations</a>
	
A resource can be represented in different ways.
A client can ask for a representation in json, xml, raw representation (stream of the image) or anything that the server can support.
The accept http header is a perfect tool to describe to the server the format exptected by the client.
	
### <a name="uniformity"/>Uniformity of the interface</a>
	
This is what makes REST so different from xml rpc. The VERBS are already defined, there is no need to invent custom verbs.
		
- GET on /resources to list the ressources
- GET on /resources/123 to read the resource
- HEAD on /resources/123 to check for the resource existence

- POST on /resources to create a new one (the server returns the created URL in the location header)
- PUT on /resources/123 to modify an existing one.
- DELETE on /resources/123 to delete it.
		
### <a name="connectivity"/>Connectivity</a>

This is one of the parts that makes the client generic and decoupled to the server.
The server gives the client the URLs needed by the client to access its resources.
It also gives the way the client should POST/PUT (by using forms) to modify its resources.

Basically, the client never hardcode how to access or modify a resource.
The main advantage is that the client will break much less than if all this information was hardcoded.


From the root url (/), the server should give the accessible urls that the client can query or send commands to.
After that, each resource should have links for other related resources.

Ex: Let's say we do a GET /organizations/123.json
	A connected json representation for an organization could look like this:

```javascript		
{ 
	id: 123,
	name: "Ziliko",
	users:{
		url: "/organizations/123/users",
		list: [
			{ name: "bob", url:"/organizations/123/users/1234" },
			{ name: "tony", url:"/organizations/123/users/1111" },
		]
	},
	url: "/organizations/123",
	forms:[
		{ method: "PUT", action: "/organizations/123",
			inputs:[
				{ id: "name", type:"string" }
			]
		},
		{ method: "POST", action: "/organizations/123/users", 
			inputs:[ 
				{ id: "name", type:"string" },
				{ id: "email", type:"email" }
			] 
		}
	]
}
```

### <a name="stateless"/>Statelessness</a>

This constraint is to avoid scaling problems, standardize development, maintenance and api.
Also, it is to ensure that all the state of a resource is accessible and consistent through an URI.

## <a name="real-world"/>The real world and what we will focus on for now</a>

## <a name="examples"/>Where can you find examples</a>