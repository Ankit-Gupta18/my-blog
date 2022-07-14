+++
categories = ["GSOC"]
date = 2022-06-25T19:32:00Z
description = "Gsoc experience chapter one"
image = "/uploads/12-removebg-preview.png"
tags = ["Internship", "GSoC"]
title = "GSoCpedia 2022: Chapter Three"
type = "post"

+++
> “Don’t worry if it doesn’t work right. If everything did, you’d be out of a job.”
>
> \~ Mosher’s Law of Software Engineering

I would like to start this blog with one of the stories shared on the WaterCooler by James.  
Early in his career, he worked in an aviation company in the UK. The project was related to the network connectivity of the airplane during its entire journey. The code was written. The code was tested by flying the plane through the UK. Everything seemed to be working fine. Now the interesting part, during an international journey the network connection was working just fine until it suddenly disconnected completely. When the flight landed, the development team was called to figure out what went wrong. Turns out the flight passed through the equator (latitude: 0) leading to the divide by zero error!😱  
_Moral: The importance of testing is real_ ✨

### Highlights

#### Week 5 - 6(11th - 25th July)

* Added a Welcome page at the beginning of the Edit Request Wizard with guidelines to follow in the process.
* Created a ping route (GET /ping) which returns some simple response so that we can easily verify via web whether the service is running.
* Written a cron job that hits this ping endpoint every 15 minutes, and sends out an email to tool maintainers if the server is found to be not running.
* Written a GitHub action that automatically deploys code to toolforge whenever you commit to the main branch (it would ssh into toolforge and run git pull + npm install + webservice restart)

      name: Deploy to Toolforge
      
      on:
        - push
        - workflow_dispatch
      
      jobs:
        update:
          runs-on: ubuntu-latest
          steps:
            - uses: actions/checkout@v2
            - uses: garygrossgarten/github-action-ssh@2b10f41b5a33808f6d24eafd253296766308b7c4
              with:
                command: >-
                  become edit-wizard bash -c '
                    cd Edit-Request-Wizard/Backend;
                    git pull;
                    npm install;
                    webservice --backend=kubernetes node12 restart;
                  '
                host: login.toolforge.org
                username: ankitgupta
                privateKey: ${{ secrets.TOOLFORGE_PRIVATE_KEY }}
                passphrase: ${{ secrets.PASSPHRASE }}
       