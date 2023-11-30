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
