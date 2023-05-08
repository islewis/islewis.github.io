---
layout: post
title: "How I've been using GPT"
author: "Inela"
tags: ["gpt", "llm", "content"]
---

# How I've been using GPT

In the last few months, anyone who has been paying attention has heard of GPT, and their parent company, OpenAI. GPT-4 was just released just a few months ago, with an order of magnitude more parameters than it's previous version. While we've seen other technically impressive Generative AI products in the past, none have captivated the mainstream's attention as much as ChatGPT, the GPT chatbot. Between a $10 Billion Microsoft investment, and being the quickest product to reach 100M users, it's fair to say more than tech nerds have heard of GPT.  While it's cool to have public eyes on cutting edge tech, and it's fun to receive texts from your mom about "chatGBT", I've been having a hard time figuring out what GPT means for me. 

Nerds of all flavors of have taken interest in these newly proficient LLMs. At any given time, I wouldn't be surprised to see a ChatGPT announcement, an opinion piece on how we'll all lose our jobs, and a criticism of OpenAI's capped profit structure all on the frontpage of Hackernews. The current environment seems to have the perfect mix of tech, entrepreneurialism, and philosophy to get everyone (and in my case, their moms) interested and talking about it. While everyone knows that these LLMs, GPT in particular, are interesting, most of the potential i've seen so far has been integrating them with existing products- I have to admit, up to this point i've thought of ChatGPT as nothing but a novel demonstration of OpenAI's capabilities. I recognize the technical prowess in the implementation of "write me an essay for my english class", and enjoy the gimmick of "write me a haiku in an australian accent", but nothing i've seen has made me jump out of my chair in eagerness to directly interface with their model for my own workflows. 

Now, I really do understand how powerful these models are (as much as anyone can), which makes it strange I've had some hesitancy using them. The only explanation that feels apt? I have a lack of imagination. The following examples are a hands-on exploratory way for me to identify the value GPT can bring to my common workflows. You might have heard the saying “If you have a question, someone else probably does too”. I have lots of questions, and this is my attempt at starting on the answers. It’s almost impossible that everything that brings value to me, will also to you, my reader, but I believe there’s still value in trying.

## Putting GPT to work

Now, I really do understand how powerful these models are (as much as anyone can), which makes it strange I've had some hesitancy using them. The only explanation that feels apt? I have a lack of imagination. The following examples are a hands-on exploratory way for me to identify the value GPT can bring to my common workflows. You might have heard the saying “If you have a question, someone else probably does too”. I have lots of questions, and this is my attempt at starting on the answers. It’s almost impossible that everything that brings value to me, will also to you, my reader, but I believe there’s still value in trying.

Once I got GPT setup in a familiar environment, I got crackin. After a month, my takeaway is GPT is fucking cool.

## What the hell can I use GPT for?

## - Fake data
GPT is incredible for creating sample data. It seems to hit all of the strengths of GPT, without running into any of the downsides, although i've found it to be a bit finicky sometimes 

```bash
$ ggpt prompt "output a csv of 3 users."

Im sorry, as an AI language model, I don't have access to a database or any specific user data
to output as a CSV file. Can you please provide more details about the user data you would like
me to generate as a CSV file?
```

I've found the workaround here to be adding the word "sample" to the query.

```bash
$ ggpt prompt "output a sample csv of 3 users."

john_doe,johndoe@email.com,28,software engineer
jane_smith,janesmith@email.com,35,marketing manager
mike_jackson,mikejackson@email.com,42,teacher
```

Pretty neat, let's add some features to the data.

```bash
$ ggpt prompt "output a sample csv of 3 users. Include email, username, name, age, and sex"

john@example.com,johndoe,John Doe,32,Male
jane@example.com,janedoe,Jane Doe,28,Female
james@example.com,jamesbond,James Bond,45,Male 
```

Lesson here seems to be that we can get pretty specific with what we want, and GPT gives it to us- Not super surprising, but good to know. GPT isn’t very imaginative with the emails or usernames, but that's probably fine.

Obviously with 3 entries this data is a bit useless, but it’s not hard to see the value here. One possibility I can see is using a data schema for production users in order to get “imaginary” users to develop against. This would allow for data that behaves correctly during development, but doesnt risk end-user data by pulling it onto dev machines. Could also be used to pipe this mostly-realistic generated data into a fuzzer for some high quality fuzzing.

## - K8s yamls
I’ve spent too much time fiddling with Kubernetes yamls. If GPT is so smart, let's try to make this process happen a bit quicker.

```bash
$ ggpt prompt "generate me a kubernetes yaml file that deployes one uubntu container, in a
namespace named ubuntu"

apiVersion: v1
kind: Namespace
metadata:
  name: ubuntu
---
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-container
  namespace: ubuntu
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command: ["sleep", "infinity"]
```

Does this pass the eye test? GPT doesn’t falter, despite my “uubntu” typo. It creates us a namespace named ubuntu, and a pod named ubuntu in said namespace. Pretty much what we asked for, albeit with some weirdness. It’s unlikely this would actually work given the versionless “ubuntu” image name, and the sleep infinity command is a bit unexpected. I also don't really think there's a ton of value in this example anyway: I could find a simple boilerplate like this with a quick google search. Lets try something with a bit more meat to it.

```bash
$ ggpt prompt "Generate me a kubernetes yaml. Include a deployment of 2 postgresql pods,
deployed into an already created namespace named thisnamespaceexists. Put it behind a service
named psqlservice. Give each pod a limit of 200MB of memory"

apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgresql
  namespace: thisnamespaceexists
spec:
  replicas: 2
  selector:
    matchLabels:
      app: postgresql
  template:
    metadata:
      labels:
        app: postgresql
    spec:
      containers:
      - name: postgresql
        image: postgres:latest
        resources:
          limits:
            memory: 200Mi
        env:
        - name: POSTGRES_USER
          value: postgres
        - name: POSTGRES_DB
          value: postgres
        - name: POSTGRES_PASSWORD
          valueFrom:
            secretKeyRef:
              name: postgresql-secret
              key: password
        ports:
        - name: postgresql
          containerPort: 5432
---
apiVersion: v1
kind: Service
metadata:
  name: psqlservice
  namespace: thisnamespaceexists
spec:
  selector:
    app: postgresql
  ports:
  - name: postgresql
    port: 5432
    targetPort: 5432
  type: ClusterIP
```

Woo. We have a deployment of 2 postgres pods, in the correct “thisnamespaceexists” namespace. It gave it the correct limit, even changing my input of “200MB” to the proper “200Mi” definition. All of the labels seem to match up, and the env vars look familiar. The service has the proper name, and what I would assume to be the proper ports. I wouldn't feel confident enough to put any money on this yaml working on the 1st or 2nd try, but given it’s passed the eye test with flying colors, there's certainly some value here. Once given my specific configuration requirements, I can start to see GPT providing much more than a quick google.

## - Code/scripts
Another use I've had moderate success with is generating quick and simple scripts. Lets take a look at some bash.

```bash
$ ggpt prompt "output a bash function that takes one integer argument named port. output
the name of the service that is running that port"
```
```
Heres a possible solution using the `lsof` command:

port_service() {
    local port=$1
    local service=$(lsof -i :$port | awk 'NR==2 {print $1}')
    echo "Service running on port $port is: $service"
}

This function uses the `lsof` command to list all open files and sockets, filtering by the given port. The result is piped to `awk` to extract the second row (which corresponds to the process ID) and print the associated command name. The output is then echoed with a message indicating the target port.

You can call this function with a port number, like:

$ port_service 80
Service running on port 80 is: httpd
```

To start, for a script this short, i'm not sure I need that much explanation. Next time, i’ll append a “Include no explanation” to my query, in the hopes of just getting the script.


But with regard to the actual script- I’m not a bash wizard, but the script passes my eye test. We know GPT can, and will, make up data, so we need to verify this somehow. To test it, let's get a psql container that will act as our target, opening up a listener on port 5423.

```bash
$ docker run -e POSTGRES_PASSWORD=password -d postgres 
b1e6e2160a251043ed3831e162fed74a88f50b6112054a018c295e20ccb47c97

$ docker ps
CONTAINER ID   IMAGE    ...    PORTS    ...
b1e6e2160a25   postgres ...    5432/tcp ...  
```
Okay, we can now validate our script against the `5432` port. If I had been smarter and included the "no explanation" with my prompt, I could have used `ggpt last` to feed the previous ggpt output into a function definition, but with the extra text I'll need to copy and paste- oh well. 

We'll define the function, and if it works as expected, we should be able to run `port_service 5432` in bash and get some sort of indication that the service behind it is postgres.
```bash
$ port_service() {
    local port=$1
    local service=$(lsof -i :$port | awk 'NR==2 {print $1}')
    echo "Service running on port $port is: $service"
}

$ port_service 5432
Service running on port 5432 is:
```
Aaaaand, its not working. We know the port is busy, so something is wrong. Breaking down our script, it looks like lots of formatting, and one command that's the meat; Let's run `lsof -i :$port` by itself.
```bash
$ lsof -i :5432

$ _
```
Weird. Permission issue?
```bash
$ sudo lsof -i :5432
COMMAND   PID     USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
postgres 1075 postgres    3u  IPv4  29545      0t0  TCP localhost:postgresql (LISTEN)
```
Cool. Now that we know the issue is a simple missed 'sudo', lets see if GPT can fix it for us. We can take advantage of `declare -f` to spit our function definition back into GPT.
```bash
$ ggpt prompt "The following bash function will not work because it needs super user
privileges: $(declare -f port_service). Return it with the changes it needs to run. Include
no explanation."

port_service () {
        sudo local port=$1
        local service=$(sudo lsof -i :$port | awk 'NR==2 {print $1}')
        echo "Service running on port $port is: $service"
}
```
Looks like its fixed. Lets try:
```
$ eval "$(ggpt last)" && port_service 5432
Service running on port 5432 is: postgres
```
Wow- let's break down this last example. GPT gave us a function that took a port number argument, and outputs a service name. The 1st attempt gave us close to what we wanted, but after testing it we found that it assumed we had permissions that we didn't. We passed the function back to GPT, told it the issue we found, and it fixed the function for us. 

This example is a bit obtuse, as I think our need was common (simple) enough to fall into the "just google it" bucket. But I don't think anyone should allow the straight-forwardness of this implementation to take away from the significance of the process. It's not hard to imagine this same workflow on similar problems that start to grow out of Google's scope. Once we needed to fix our sudo issue, being able to pass all the context into GPT became a killer feature. In our case, this meant the entire function definition, not something we could have done with google, especially once you've grown past a simple one-liner. If I was interested in growing out this function and adding more behavior, I would continue to take advantage of this GPT feedback loop: Script + instructions into GPT -> Test the output -> Add new instructions based on test -> repeat.

## Conclusion

Overall, I was fairly impressed with the capabilities of GPT. Nothing i've shown in this article is particularly innovative or awe-inspiring, however I believe the examples here could be a launchpad for someone who is interested in adding GPT into their professional toolbox. GPT obvious has some downsides, but with the current rate of LLM innovation I have a hard time lending any of them too much thought; surely any weaknesses in GPT's capabilities will be solved soon, either by OpenAI or by their competitors. 

It's not too late to start using these tools, but there will be a point where it is. Like any significant technology, those who adopt early will disrupt those who do not. With a tool as accessible as these LLMs are, don't let your imagination stop you from capitalizing off these incredibly powerful tools.
