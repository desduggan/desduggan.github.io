---

layout: post
title: Hypermedia Evaluation

---

# What does a business gain from using hypermedia?
## Introduction
In the world of web services and API design, you can't go long without running headfirst into the RESTful design paradigm.  Not only do we see RESTful API's being implemented by technology giants such as Twitter and Google, but the last few years have seen a major proliferation of RESTful API's being developed by small and medium sized companies.  The RESTful community is extremely active, and the space continues to develop.  Hypermedia lives at the end of the spectrum of RESTful practices, and is considered the keystone to any truly RESTful design (see the image below).  (2) 

 ![Icon](http://www.desmondrduggan.com/hypermedia.png "Hypermedia Spectrum")

From a high level, we can define the REST paradigm by the 6 constraints that it imposes on the design of web API's.  Without going into detail, a RESTful API is stateless and layered, and has a uniform interface.  The hypermedia constraint is a component of the uniform-interface constraint.  Again, avoiding the deep technical nature of hypermedia, an API that conforms to this constraint will provide links for related actions or resources, whenever a request is made. 

Hypermedia is technically abstract and hard to grasp, and it can be very difficult to see the end value that it provides to the business.  The purpose of this post is to explore the real value-add aspects of having a Hypermedia compliant API.  Ultimately, I will argue that the flexible and dynamic nature of the decoupling between client and server within a hypermedia constrained API affords value in three areas: independent evolution, efficient development, and simplified client interaction.  

## Independent Evolution
> Claim #1: If a business can decouple their server api from their api consumers by means of hypermedia controls, they are able to innovate faster and have the freedom to make high level business decisions, without the expensive consequences of having a non-flexible client.  

Take a simplified Media API called MultiMedia.com that has a large database of movies, which can be browsed and purchased.  Up until this point, the Media API offered movies only.  Clients could request a list of movies for a given genre by sending a GET request to the following address: 

     (1) http://www.multimedia.com/v1/genre/Action/

Now say that this business was extremely successful because they landed big partnerships with television show producers, something they had not anticipated.  They want to incorporate the television shows into their API, but they run into an issue: if a client makes a request to the URI above, it is unclear whether they should receive a list of movies or television shows for the given genre.  The CTO and his team decide that movies and television shows should be requested at the following new URI's: 
     
     (2) http://www.multimedia.com/v1/movie/genre/Action/

     (3) http://www.multimedia.com/v1/television/genre/Action/

With a traditionally designed API, without hypermedia, it is clear at this point that if MultiMedia.com goes ahead with the change, all of their clients who were used to requesting movies at (1) will now break.  In contrast, with hypermedia controls, this change would be simple and would not cause any breakage.  Because the specific URI's are requested at runtime in a hypermedia API, the client wouldn't miss a beat.  Furthermore, hypermedia controls offer options for discovering new resources, so the clients could become dynamically aware of the new link at (3).  

#### Implications
This example illustrates the freedom product managers and business leaders have to make high level business decisions while avoiding technical complexities that come along with adding, modifying and removing features as a result of using a hypermedia API.  The business development cycle can is more agile and flexible, less time is wasted handling changes, and there is less friction between the business demands and implementation.  

## Improved Engineering Efficiency and Scalability
> Claim #2: The flexibility and dynamic nature of hypermedia controls alleviate engineering constraints caused by the static nature of traditionally designed API's, thereby increasing engineering productivity.  

The design of traditional API's necessitates API consuming clients to program against components of the API that are liable to change: most notably, the API media type and the resource URI's (see below for definitions).  When a client interacts with the API in any way, they are sending a request to a resource URI and the response comes back in the form of the API media type.  Therefore these two components are at the core of any API, and consequences of a change can be far reaching for the API consumers.  

In reality, there is a number of API's for which the media type and resource URI's will remain constant.  For these API's, the dynamic behavior of hypermedia controls will not produce much value.  However, for many API's, a change in a URI or media type is required either by business priorities or engineering constraints.  For the latter group, hypermedia controls can have a positive impact on the API development.  

#### Improved Efficiency
Specifically, in reference to claim #1, when engineers have the ability to add and remove features with hypermedia, the business realizes the cost savings of using a hypermedia compliant API in two areas: firstly, when the engineers avoid refactoring code that was designed to meet the requirements of a specific feature, and secondly, when the engineers can avoid versioning due to the resistant nature of hypermedia.  

#### Improved Scalability
Furthermore, hypermedia provides a more scalable model for both clients and API providers.  On the one hand, a hypermedia consuming client has to keep track of only one URI, the base URI, and leave the API flow to the API designers while simply using the links provided in the hypermedia response to navigate the resources.  On the other hand, API providers have the ability to link resources and modify features as needed.  


## Simplified Customer Relations
> Claim #3: Decoupling the client and server with hypermedia controls reduces the amount of customer support demanded by clients.  

In reality, there is degree of ongoing communication between the API provider and consumer.  If a API provider makes updates to their system on a four month cycle, then they will want to be communicating these changes to their clients.  Whether they add functionality or update performance, clients should be aware of such changes.  Accordingly, the business must commit resources to customer relations and technical support.  

In this context, it's possible that the provider is forced to induce a client-breaking-change, such as changing a resource URI or removing a resource property, and must communicate the change to all of their clients.  From a customer relationship management standpoint, this can be a very expensive task, some clients will be very resistive to change.  

Although hypermedia API's certainly don't prevent all issues that come along with client-breaking-changes, they are much more flexible than traditionally designed ones.  For some changes, such as adding features or modifying resource URI's, hypermedia API's completely eliminate the need to upgrade clients.  For more difficult changes such as resource property modifications, hypermedia controls provide additional methods of communicating change to the clients such as resource property meta data in the API media type.  


## Drawbacks to Hypermedia Controls
1. Hypermedia API's take more time and planning to successfully implement.  

2. Clients must understand how to work with a hypermedia response. 

3. Caching becomes more important because the API server is stateless. 

4. Despite the existence of some hypermedia specific media types such as HAL or Siren, there isn't a universally accepted media type yet.  


## Conclusion
Hypermedia API's can provide value for both clients and API providers, but quantifying the gains is difficult to do.  I have listed three primary value propositions here: independent evolution, improved engineering efficiency and scalability, and simplified customer relations.  Ultimately, these gains will have a larger impact when the long term consequences are considered.  For a young, small scale API, it may be hard to justify the incorporation of hypermedia controls, due to the task of implementation and on boarding clients.  However, for large scale, multifaceted API's, hypermedia can have a strong impact on the businesses bottom line.  
