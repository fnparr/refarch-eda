# Event Storming Methodology
EventStorming is a workshop format for quickly exploring complex business domains by focusing on *domain events* generated in the context of a business process or a business application. It focuses on communication between product owner, domain experts and developers.
A **Domain Event** is something meaningful that happened in the domain.

Event Storming - a variant of Domain Driven Design - was introduced and publicised by Alberto Brandolini in [Introducing Event Storming]( 
https://leanpub.com/introducing_eventstorming ). This approach has achieved significant recognition in the Design community as a technique to accelerate capture and team communication of a solution design.  In this section we describe use of the method with adaptations to design of Event Driven Architecture solutions. 


## Conducting the Workshop
An Event Storming Workshop may be done after a Design Thinking Workshop in which [Personas](https://www.ibm.com/cloud/garage/content/think/practice_personas/) and [Empathy Maps](https://www.ibm.com/cloud/garage/content/think/practice_empathy_maps/) are developed and business pains and goals are defined. The Event storming will add deeper context on the process and the events. It will be fit well in deploying application in an Event Driven Architecture.

### Preparation
* Get a room big enough to hold at least 6 to 8 persons and with enough wall space on which to stick big paper sheets: you will need a lot of wall space to define the models.
* Obtain green, orange, blue, and red square sticky notes, black sharpies and blue painters tape
* Do not allow people to open their laptops and try to limit the number of chairs; it is important that the team stays focused and connected and conversation flows well.

### Concepts
Many of the concepts addressed during the event storming workshop are defined in the [Domain Driven Design](https://www.ibm.com/cloud/garage/content/code/domain-driven-design/) approach.
The following diagrams present the elements used during the analysis:

 <img src="evt-stm-item1.png" width="700">

Domain events are also named 'business events'.

<img src="evt-stm-item2.png" width="700">

And how those analysis elements are linked together:

<img src="evt-stm-oneview.png" width="700">

* **Actors** consume data via user interface and use UI to act on the system via commands
* **Commands** are the result of some user decision, acting on relevant data which are part of a Read model in the [CQRS](../readme.md#command-query-responsibility-segregation) pattern.
* **Policies** represents reactive logic that takes place after an event occurs, and triggers commands somewhere else. There are written on Lilac sticker and start with "whenever...". Policies can be manual step the human will follow like a procedure or guidances, or can be automated. When applying the [Agile Business Rule Development methodology](http://abrd.github.io) it will be mapped to a Decision within the [Decision Model Notation]().
* **External systems** are producing events.
* **Data** can be presented to user interface or modified by system.
Events can be created by command, external systems and data creation, by timer, ...

Finally when arranging the events in timeline it will be possible to identify pivotal events and swim lanes.

<img src="evt-stm-pivotalevt.png" width="700">

### Workshop Execution
The Goal is to better understand the business problem to address with the future application. But it can apply to search solution to bottleneck in existing application. It starts by the big picture by building a timeline of domain events as they occur during the business process life span.

Avoid to document process step, focus on events. The timeline will represent the high level sequential process.

*  **Step 1: Domain events discovery:**
Name the domain events in orange sticky note using verbs in past tense. Describe **What's happened**. At first just "storm" the events by having each domain expert generate their lists of domain events; you may not need to iniitally place them on the ordered timeline.
The events must be worded in a way that is relevant to the domain experts. You are explaining what happens in business terms, not what happens inside the implementation of the system.
You don't need to describe all the events in your domain, but it is important to cover the process from end to end.
You need to identify the start and end events.

* **Step 2: Tell the story:**
 * In this step, you retell the story by talking about how to relate events to personas.
 * Add questions when some parts are unclear
 * Document assumptions
 * Rephrase event with past tense if needed
 * Focus on happy path, the things going on, on regular time
 * Add pivotal events
 * Add swim lanes

Here is an example of ordered domain events with pivotal event and swim lanes:
 ![](evt-timeline.png)

* **Step 3: Commands:** address the why did event happen. The focus is moving to the cause and effect sequence. Command is what people do in the domain to create event.

* **Step 4: Aggregates**: Aggregates represent business concept with local responsibility and grouping events and commands. Most likely aggregates become micro service boundaries.

* **Step 5: Business Context:** it defines terms and concepts with a clear meaning valid in a clear boundary. (The term definition may change outside of the business unit for which this application is developed). The goal here is to defined the boundaries and the term definitions.

* **Step 6: Data:** Data for the user interface so user can make decision are part of the read model. For each command and event we may add data description of the expected attributes and data elements needed to take such decision. Here is a simple example for a `shipment order placed` event created from a `place a shipment order action`.

  <img src="evt-stm-data.png" width="400">

  This first level of data definition will help for assessing the microservice scope and responsibility too.

* **Step 7: Insight:** We have the need to add one element to the method to address an important dimension of modern applications integrating analytics and machine learning capabilities.

  With Event Storming so far we have been looking backwards at each event because an event is something which is known to have already happened. With this perspective when we think about data which can help an actor decide when and how to issue a command, there is an implicit suggestion that this is based on properties of earlier known and captured business events.

  With insights storming we extend the approach to also look forward by considering *what if we could know in advance that this event was going to occur*. How would this change or actions, what would we do now in advance of that event actually happening ?.

  We  think of this as generating a *Derived Event*, which rather than being the factual recording of an event *something which has happened* is a forward looking or predictive view  *Something is probably going to happen at a particular time*

  The ability to generating these derived events comes from integration with analytics and machine learning, where the event feeds can be processed, filtered, joined, aggregated , modeled and  scored to assess predictions,

  These Insights delivered as *derived* events can now be joined into our model. The parallelogram construct is used to represent this joining operations. This processing is very important to analyze as early as possible in the development life cycle, and the event storming workshop is the best opportunity.

  <img src="evt-stm-insight.png" width="700">

## Event Storming to User Stories / Epics
When developing using agile methodology, one of the important element of the project management is the user stories or epics construction. The commands and policies can be describe easily as user stories, as commands and decisions are done by actors. The actor could be a system too.
For the data we have to support the CUD operations as user stories, mostly supported by a system actor.

  <img src="evt-stm-userstories.png" width="700">

Events are the result / outcome of a user stories. And can be added as part of the acceptance criteria of the user stories to verify the event really occurs.

## Applying to the container shipment use case
To support one of the implementation solution to validate the Event Driven Architecture, we have developed the event storming and design thinking main artifacts for a [fridge container shipment process.](https://github.com/ibm-cloud-architecture/refarch-kc/tree/master/analysis/readme.md)


### Further Readings
* [Introduction to event storming from Alberto Brandolini ](http://ziobrando.blogspot.com/2013/11/introducing-event-storming.html#.VbhQTn-9KK1)
* [Event Storming Guide](https://www.boldare.com/blog/event-storming-guide/)
* [Insight storming Guide](InsightStorming/readme.md)
* [Wikipedia Domain Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design)
* [Eric Evans: "Domain Driven Design - Tacking complexity in the heart of software"](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software)
* [Patterns related to Domain Driven Design](https://martinfowler.com/tags/domain%20driven%20design.html) by Martin Fowler
