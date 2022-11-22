# Chat-Api App

This app is built using rails-6.1.4.1 and uses a MySQL database. It integrates with Elastic Search, SearchFlip, Redis, and SideKiq.

## Installation
> Before you install this app you should insure that you have `ruby-3.1.2` or higher installed.

## To run this app follow this steps

* Clone the app from github.
```bash
git clone  
```

* cd in the repo directory.
```bash
cd chat-api
```

* Install dependencies by running.
```bash
bundle install
```

* Create db and migrate schema.
```bash
rails db:create
rails db:migrate
```

* Run the rails server.
```bash
rails s
```

* Now you can access the app apis by visiting [localhost:3000](localhost:3000).

## Using Docker

* Start by using this command and wait for it to finish
```bash
docker-compose up
```

* Then go to localhost:3000 on your browser and press on run pending migrations

### Time to create applications, chats, messages, search for messages, and wait an 1 hour to get the count of messages in a room

* First we will open another terminal and get the container ID of the chat-api-web
```bash
docker ps
``` 

* When we get the container id we will add it to this code and run the rails consel "note: try first running it then exit then run it again make sure it gives you this(2022-11-22T18:46:46.709Z pid=29 tid=2h5 INFO: Cron Jobs - added job with name: Update apps' chats_count - every 1hr
2022-11-22T18:46:46.714Z pid=29 tid=2h5 INFO: Cron Jobs - added job with name: Update chats' messages_count - every 1hr
Loading development environment (Rails 6.1.7))
```bash
docker exec -ti {container id} rails c
``` 

* From here we can start creating (after creating go to http://localhost:3000/applications )
```bash
Application.create(name: "ChatApp1")
``` 

* This will generate a token for us to go to the chat time to create a chat with the application id (after creating go to http://localhost:3000/applications/[application Token]/chats/1)
```bash
Chat.create(number: 1, application_id: 1)
``` 

* Time to create some messages with the chat id (after creating go to http://localhost:3000/applications/[application Token]/chats/1/messages)
```bash
Message.create(body: "Hello", chat_id: 1,id: 1, number:1)
Message.create(body: "Hello World", chat_id: 1,id: 2, number:2)
Message.create(body: "Tell Us", chat_id: 1,id: 3, number:3)
Message.create(body: "Let's Gooo", chat_id: 1,id: 4, number:4)
``` 

### Time to try and work with the search

* In you browser go to (http://localhost:3000/applications/[application Token]/chats/1/messages/search/[The word you are searching for])

* It will show you the message with the word you searched for

### Wait for an hour to get the messages_count 

* In your browser go to (http://localhost:3000/applications/[application Token]/chats) you will find that it will count the messages created at the consel that we created above

## This is the end of the chat-api by ruby on rails