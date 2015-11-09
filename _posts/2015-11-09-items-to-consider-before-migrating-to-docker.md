---
layout: post
title:  "Items to consider before migrating to docker"
date:   2015-11-09 22:18:00
categories: devops, programming, functional-programming
comments: true
---
1. **First consider the exact reasons you adopt `docker`**, or better, in it's generalized form - for adopting `containerized` packaging and deployments methodology.  Believe it or not, it's easy to get mislead by all the rumours spread around.  A good answer for the question, why am I changing my deployment architecture to containerized based deployments would be that you are a developer who appreciates with caution the concept of immutability and `functional-programming`.  In this case `containers` allows you to deploy these concepts into your deployments.  Having `containerized` deployments allows you to have `immutable deployments` in a much easier and fun way.  By having your containers `read-only` you may even come closer to the concept of `pure deployments` where you do no modifications but only replacements.  A mostly bad answer would be because you think it will improve the performance of a certain server.  Having that issue solved let's move on the next items to consider before you take action.  *the game where you push one thing and another one pops out hopefully with one eye out*

2. **Are you ready for immutable deployments?** In the previous item we dealt with the motivation to adopt `docker`, lets now check how ready you are for this new methodology.  Questions to ask: Do you install your apps from scratch, is that already happening in production? If not - are you at least already deploying your apps into `VM's`, or, even better to `cloud-vm's`?  Do deployment/production team add new instances of your app without contacting the relevant developers team as if they do not exist? If I restart your apps now will all behave as usual (the usual without problems)?  If you answered yes to at least some of the above, then, the effort of moving into containerized deployments is achievable with much less frustration.  If not, you should first review your deployments, update them, or be ready for much more work when using container based deployments.  (Note, if you plan to mutate your environments with containerized based deployments you are heading the wrong way) *put someone with his finger out measuring the air heat*

3. **What are you going to do with the current deployment tools such as `puppet`, `rpm` and the like** On one hand using these tools is great, because this means your deployments are very close to fully automated (or fully automated).  On the other hand this means that you have a choice to make.  Either dump them and use a single container package builder (`Dockerfile`) or else continue using your `rpm` scripts together with `docker` scripts, and same for puppet.  Personally try to get things simple on this matter, if you can have a single scripting language, go for it, if you already have too much infrastructure around `rpm` consider keeping it.  Note that if you continue having the bulk of packaging in `rpm` this would mean you should aspire to being able to install your packages even without `docker`.  As for `puppet` you should highly consider replacing it all together by `docker` scripting an its peripheral scripts (`kubernetes`).  *two dogs running one after another one named puppet and one named kubernetes*

3. Training - you would need to train your developers / qa / support on docker, even in cases where you don't plan to use docker in dev/qa (and you should) then they would still need to investigate issues in production, its not going to be a good idea that the troubleshooters won't know the environment on which their servers are running, good understanding that is.  *someone doing pushups or lifting his laptop up and down when he lies down as if those are mishkolot*

4. Which app types would you need to orcehstrate? do you have stnarard servers (http style), storm topologies? hadoop jobs? maybe you already use `YARN`? Each orchestration type would require an effort from your side.  Our recommendation is to go with `kubernetes` as the de-facto orchestration tool.  It's also possible to [integrate](http://hortonworks.com/blog/docker-kubernetes-apache-hadoop-yarn/) it with YARN.



3. **Tagging Convention** now that you attach proper tags to your build you need to think of good tagging convention practice.
4. Note that as one of the main things we want to get out of docker or any other container is to prevent server drift, if you are already in a state where you are as immutable as you can in your server installations then you are in a good position.  If you are far from it first check how different are your servers one from another (which are supposed to be the same if they are running same app) if they are different then first check if by having them all the same your services are still behaving the same, this will have you much closer to being able to run docker with less issues at first.
2. logging.
3. Tagging labeling docker tag should just be the vesion name or latest registry is global and repository is for the project
3. configuration for minimal configuration like one parameter pass it as argument, for a few more pass them as environment variable, always prefer to have convention for example if you use some cassandra host simply refer to DNS CASSANDRA in dev would be the right one in prod the right one.  For more complex configuration consider storing them in some kind of database or in volume files.
4. monitoring the containers.
5. performance tuning.
6. using linux.
7. already using puppet? rpm? now you are going to have another scripting language docker md.
8. You could even increase security by having a container read only! nothing can write to it.  security audits can be faster all these apps are read only.
9. docker vs swarm vs kuber http://radar.oreilly.com/2015/10/swarm-v-fleet-v-kubernetes-v-mesos.html
10. What about rollout maybe consider the non rolled out services as all kubernetes service which will hide they are not a service its just an abstraction.
11. You can have another container the first one we don't need tcpdump and tcpflow and the other container will include these services which would mean you can listen to its ethernet without introducing security issues.
