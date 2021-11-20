# Week1 - Publish Streaming Data into PubSub

- Google PubSub is a fully-managed real-time messaging service that allows to send and receive messages between independent applications. 
- Can be used to publish and subscribe to data from multiple sources.

## Create PubSub topic and subscription

1. Create topic sandiego
```
gcloud pubsub topics create sandiego
```
> Created topic [projects/qwiklabs-gcp-01-340bd15aed47/topics/sandiego].

2. Publish a simple message
```
gcloud pubsub topics publish sandiego --message "hello"
```
> messageIds:
> - '3414701126791240'

3. Create a subscription for the topic
```
gcloud pubsub subscriptions create --topic sandiego mySub1
```
> Created subscription [projects/qwiklabs-gcp-01-340bd15aed47/subscriptions/mySub1].

4. Pull the message that was published to the topic
```
gcloud pubsub subscriptions pull --auto-ack mySub1
```
> Listed 0 items.

We notice that result is listed as 0 items.
> This is because the subscription subscribed to the topic after the message was published.

5. Publish another message to the topic
```
gcloud pubsub topics publish sandiego --message "hello again"
```
> messageIds:
> - '3414731669901248'

6. Pull messages published to the topic
```
gcloud pubsub subscriptions pull --auto-ack mySub1
```
> ┌─────────────┬──────────────────┬────────────┐
  │     DATA    │    MESSAGE_ID    │ ATTRIBUTES │
  ├─────────────┼──────────────────┼────────────┤
  │ hello again │ 3414731669901248 │            │
  └─────────────┴──────────────────┴────────────┘

Now we can see the result as the message was published after creating the subscription.

7. Deleting a subscription
```
glcloud pubsub subscriptions delete mySub1
```
> Deleted subscription [projects/qwiklabs-gcp-01-340bd15aed47/subscriptions/mySub1].

8. Deleting a topic
```
gcloud pubsub topics delete sandiego
```
> Deleted topic [projects/qwiklabs-gcp-01-340bd15aed47/topics/sandiego].