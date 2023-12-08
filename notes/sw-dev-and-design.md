# Design for Maintainability

## Function / Nonfunctional requirements

### functional req

**Functional** requirements specify **what** the software should do. They describe the functionalities of a system, such as a business process, data manipulation, user interaction, media processing, calculation, or any other action that the system can perform. Functional requirements can be measured in "yes" or "no" terms and usually include the words "can" and "shall."

Functional Requirements:

- **User stories** are short descriptions of functionalities, as seen from the end-user perspective. They focus more on how the user interacts with the system and what they expect the goal of the interaction to be, rather than what the system does, but since the software is often very domain-specific, they help you to understand the system better as a developer.

- In contrast to user stories, **use cases** focus less on the user's interaction and more on the cause and effect of actions. If a user story stated, "A user can save documents by clicking Save," the related use case would state "When the Save button is pressed, the current document is saved to the server's NoSQL database and to the client's local cache."

### Nonfunctional req

**nonfunctional** requirements tell you **how** a system **should** perform those actions. You can also think of them as **quality attributes**. Nonfunctional requirements often use the words "must" and "**should**" and are commonly measured over an **interval or a range**. describing expected behavior over a range of time.

Nonfunctional requirements specify the quality attributes or technical requirements of the system.

They are more related to the system's architecture than its functionalities and are often constraints on the technical properties of a system. Important in testing and delivery. 

In the long term, it is common to see that the nonfunctional properties of the system become the main reason an application succeeds or fails. Therefore, it is often said that nonfunctional requirements correlate strongly with the application quality

## Maintainability Through Design

SOLID is an acronym for five software design principles:

- **Single responsibility principle**: One class should have only a single responsibility.
- **Open-closed principle**: Components (classes, methods, and so on) should be open for extension but closed for modification.
- **Liskov's substitution principle**: Derived types must be completely substitutable for their base types.
- **Interface segregation principle**: Clients should not be forced to depend upon the interfaces they do not use.
- **Dependency inversion principle**: Program to an interface, not to an implementation.

example: **S**
This class violates the single responsibility principle because the class NetworkService has two responsibilities.

First, it takes care of setting the class parameters, set_name, and set_config, in addition to deploying the service itself, deploy_service. Any changes to the deployment process could cause changes to the NetworkService class, which are not needed.

For this example, the NetworkService class should only be responsible for setting data for the service itself.

An extra class NetworkServiceDeployer will be responsible for deploying the service.

In practical terms, this allows two developers to work on these classes. One can change how the service parameters are set, while the other one can change how the service is deployed, all without affecting each other's work.

The facade pattern is commonly used alongside the single responsibility principle. It hides the complexity of the underlying code by providing context-specific interfaces.


class network
init
values
deploy
    execute deploy config <- this should be in a separate class, violate single responsibility.

instead use **Facade** pattern:
class network
init
    self.deployer = NetwServDeploy()
    ...

class NetwServDeploy()
init
...

**O**
- have multiple smaller sub classes rather than one huge class.\
In practical terms, the open-closed principle means that additional features can be added without changing the underlying source code, while still using it. You should not have to modify any classes, interfaces, or other components to add a new functionality.

**L**
example:
class returns a string, when class above it expecting to return an object, stay compatible with superclass. child class never change characteristics. such as arguments or return types.

**I**
ex:
class NetwUser(NetwSvc):
def get_user(self):
    return DB.get_user(self)
def get_infra_config(self:)\
    raise NotImplementedError <- if you call this interface it will just return error. instead **only define the part you need**
    if you make changes to the original module, you don't need to make chagnes in the clients which use that module. 

**D**
ex:
separate low level and high level classes. abstractions? -really bad explanation in video 2 on **D**. 

CLass NetworkService:
    ...
Class Router_IOS(NetworkService): - inherits, but a

### Feedback:
content review question 
all code snippets in one line unreadable (`Maintainability Through Design`) :
<https://ondemandelearning.cisco.com/apollo-alpha/mc_devcor20_01/pages/4>
Which code snippet adheres to the open-closed principle?
voice actor accent difficult to understand. does not explain through examples well, came up in SOLID principle, reading was better than watching video. 

## Matinability through design
DRY = Don't Repeat yourself
    - each class / func / etc have a unique purpose

### Feedback 
content review question with python hard to read with text all in one line again `Which code snippet adheres to the DRY principle?` and example D is in the middle and says none of the above.

## Modularity in Application Design

Modular applications ideally have high cohesion and low coupling. A high cohesion means that the elements of a specific module belong together by functionality, data types, and so on. Low coupling states that the modules are largely independent of one another. Interactions between modules should be kept to a minimum but should be plentiful inside a module.

In contrast, modules with low cohesion often make function calls to other modules, while seldom using the module's internal functions and classes.

Modular software design enforces the following software qualities:

Composability: The idea of composability is to produce software from reusable modules. The modules should work in an environment different from the one in which they were developed. Composed software should also be a reusable module itself.

Decomposability: Decomposability is a scale of how easy it is to break down a problem into subproblems, connected by simple interfaces. The communication between problems should be minimized so work on each problem can proceed independently.

Understandability: This trait defines how easy it is to understand and learn to use a module.

Continuity: Continuity states that the smaller the change in the specification is the fewer modules need to be changed. This goes hand in hand with the single responsibility principle. If each module does one thing and does that one thing well, the number of changes for each change request is minimal.

Protection: Modular protection is satisfied if faults that occur in a certain module stay confined to that module. In more practical terms, an error in Module A should not break Module B. This does not mean that an error cannot be raised in Module A and handled in Module B; for example, if an API call failed in Module A, but the failed API call is handled in Module B, this Module A error would be handled by Module B since the call passes control from Module A to Module B.

In addition to considering the previously mentioned software qualities, module designers also should adhere to certain rules:

Direct Mapping Rule: The structure that is used in the implementation of a software system should remain compatible with the structure used for modeling the system. If a clear model of the system exists, a direct mapping is needed to ensure that no data is lost in the implementation and that any potential changes are easier to implement, which benefits continuity.

Few Interfaces Rule: Every module should communicate with as few other modules as possible.

Small Interfaces Rule: When two modules communicate, they should exchange as little information as possible. This and the previous rule aim to reduce the amount of communication between modules, which reduces the overhead and complexity.

Explicit Interfaces Rule: When two objects are communicating, this must be obvious in their class definitions. The conversations need to be clearly visible. This rule benefits composability and decomposability since if you need to decompose a module into many submodules or compose it from several other modules, clearly visible connections make it easier.

Information Hiding Rule: Each module must have a limited subset of properties and functionalities available to the public; the rest should be secret. This is commonly achieved in code by making some classes public and making others private. By reducing the number of public functionalities, you increase the number of modules that can change without affecting the clients. The bigger the public part, the greater that chance is.

## Dependency Injection (software design pattern)

Dependency Injection pattern talks about decoupling logic and dependencies by injecting them, rather than instantiating them.

Dependencies in software can be any objects or data that are required for another piece of software to function. One way of structuring the providing of dependencies is to embed the logic for instantiating or locating the dependency directly inside the code that requires it. Another way is to let the client declare its dependencies and have an external piece of code provide or inject them—dependency injection.

The goal of dependency injection is to achieve **Separation of Concerns**. Separation of concerns is a principle that tries to separate an application into unique sections so that each section manages a specific set of information (a concern). Separation of concerns is a baseline for some other software qualities, such as modularity.

ex: HTML + JS + CSS each complement and do differnt things.

Dependency injection defines four different roles within its domain:

**Service**: An object that can be used. (acts a dependency)

**Client**: An entity that uses said service.

**Interface**: Defines how the client may use the service.

**Injector**: Constructs the service and injects it into the client.
One of the biggest benefits of dependency injection is the ability to test the client independently of the service.
works well with microservices
looser coupling, harder to navigate code and complex. easier to test

### Feedback
needed to click through videos even though didn't watch to mark as completed.

# Designing for Serviceability 

## Observability in App Design

3 questions of an app for observability:
- What is the app doing? (events / actions errors)
- what are the supporting systems doing? (hw / memory / db queries)
- what are the users doing? (docs help steer)

## Scalability in App Design

Horizontal scaling: 
Functional scalability: Do more without disrupting existing services.

Geographical scalability: Stay effective while expanding geographically.

Load scalability: Increase load on individual components.

Administrative scalability: Support more users or tenants.

Generation scalability: Be able to adapt to newer components.

Heterogenous scalability: Be able to adapt to different vendors.

Vertical scale: scale up/down, more mem /storage

3 Infra archs:
- share nothing, each service has its own data 
- shared disk/db arch, shares dissk, needs locking system to prevent race condition concurrent writes, can become choke points
- shared everything, maximize resource util. can bottleneck storage/memory. 

## High Availability & Resilency

3 principles:
- elimination of single points of failure
- detection and handling of failures
- reliable crossover mechanism

Making code more reslient:
- retry loops, retry with longer and longer delays, idempotent actions
- fallback mechanisms: return to default value if fail to get value from another part. predefined or cached
- implementing timeouts: wait for fail
- circuit breaking: isolate failures, wrap code and if fails, for example if a service is offline, fail and wait until back online

## Latency and rate limiting
caching content with CDN
pagination for resource loading
lazy loading: resources loaded only when needed (init does nothing)

## Architectual Patterns

Monolithic: UI/Business Logic/ Data interface all in one. Single-Tier, you can scale, but replicate whole app. all dev done in single stack often like Java or NodeJS. development faster. updates and new languages tough

Service-Oriented Architecture (SOA): 

older, uses Enterprise Service Bus to share communication channel. precurser to microservices. services use contracts to communicate with each other. XML and SOAP common. the service bus can become bottleneck. 4 types of services (business, enterprise, application and infra)

Microservices:

each microservice is separate functinality and the implementation is hidden to others. only input / output format needed. fault isolation easier. 
greatly increase complexity, creating a distributed system. partial failure must be handled. end to end tests are harder, issues can happen in connecting the services. 2 types of services (functional and infrastructure)

Event-Driven Architecture:

creating / consuming / reacting to events (significant state change). event sent to event consumers to trigger reactions. Middle-ware with Event Broker (placed in queue and dispatched to event processor) and Event Mediator (cooridanted to process )

## Sequence Diagrams

One of the main components of these diagrams are participants. Participants are the individual components that interact with others within the model. Participants use the notation of “ObjectName:className" as you can see in the example of "P1:Participant," where P1 is the instance object name and Participant is the class name. If the instance name of the class is irrelevant, it can be skipped and that participant is displayed simply as ":Participant."

an **actor** interact with the application, users. can also be an API service.

Each participant has its own **lifeline**. A lifeline indicates the participant's presence and activity over time. They can become activated, displaying that they are busy executing a task or waiting for a message. A narrow rectangle denotes an activated lifeline, as you can see in the example of an Actor's lifeline after sending a Request and before receiving a Response. When a participant is no longer busy, its lifeline becomes deactivated.

Interactions between participants are conveyed by **messages**, depicted by arrows between participant's lifelines.
Grouping operators are used to create combined fragments—logical groupings that contain conditional structure, represented by a rectangle in the sequence diagram. Each combined fragment is composed from one or more interactions and interaction operator.

The "opt" operator works as a simple IF statement.

The "alt" operator is used for IF...ELSE..THEN statements and can have as many conditions as are needed.

Loops are created with the "loop" operator. To break the loop prematurely, the "break" operator can be used. Break is also used to handle errors in the application flow.

Finally, the "par" operator depicts parallelism. All the fragments inside this combined fragment are executed in parallel.

A good practice is to use an Entity-Control-Boundary (ECB) pattern, which is a variation of the Model-View-Controller (MVC) pattern that also encapsulates some business logic.

An Entity is an object that represents some meaningful chunk of system data. It correlates to an MVC model, such as a Customer entity.

Control objects represent MVC controllers and manage the flow of interactions between boundaries and entities. They manage the processing and execution of the commands coming from a system boundary.

Boundaries represent MVC views and are responsible for interaction with external actors, such as a form on the user interface.

## Lab: Construct a Sequence Diagram

