# Cloud Events Orchestration (workflow) Examples

This repository contains a set of examples showing how a Workflow Engine can be used to Orchestrate Cloud Events.

For these examples you will be using Kubernetes, Helm and Zeebe. 


# Example
Let’s imagine that we have two services to deal with customers wanting to buy tickets for music concerts on our website. Most of these systems are required to handle high loads when a new concert goes online, as fans might want to buy all the tickets in a short period of time. 
The website and customer flow look like this: 


In the backend, there will be a service in charge of queuing customers that want to buy tickets and a payment service in charge of processing the payments. Due to the high demand, timeouts need to be in place to make sure that customers that are not willing to buy the tickets get removed from the queue if they spend too much time deciding. 



These two services have been designed with an Event-Driven Architecture in mind, so they emit events and react to events. The following events are consumed and emitted by the TicketsService: 
Tickets.CustomerQueueJoined: A customer is interested in buying a ticket so they have joined the queue to buy tickets 
Tickets.Requested:  A customer has selected one or more tickets for the concert and is ready to checkout. 
Tickets.CheckedOut: A checkout action was confirmed by the customer.
Tickets.Emitted: the tickets have been emitted to the customer. 
Notifications.Requested: A notification was sent to the customer. In our example, this can happen due to time outs while checking out the tickets or due time out from the payment service while authorizing the payment. 
On the other hand, the PaymentService can react and emit the following events:
Payments.RequestReceived: A payment request has been received and it is queued to be processed. 
Payments.Authorized: The payment was successfully processed and authorized.


By looking at these events you can quickly realize that the interactions between these services and the Customer on the website are asynchronous. Events are emitted and some other service will react and process them, probably emitting another event as a result.  

In the following sections, an Orchestration approach is introduced without changing our service, and we can tackle the points mentioned in the introduction (Visibility, Coordination, Error Handling, Compliance). 


# Source Code:
- Zeebe Cloud Events Router: http://github.com/zeebe-io/zeebe-cloud-events-router/
- Tickets Service: http://github.com/salaboy/tickets-service
- Payments Service: http://github.com/salaboy/tickets-service

# How to run the examples: 

Find the instructions here: https://salaboy.com/2020/05/18/orchestrating-cloud-events-with-zeebe/
