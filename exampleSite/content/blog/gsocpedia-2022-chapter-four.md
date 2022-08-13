+++
categories = ["GSOC"]
date = 2022-06-25T19:32:00Z
description = "Gsoc experience chapter three"
draft = true
image = "/uploads/14-removebg-preview.png"
tags = ["Internship", "GSoC"]
title = "GSoCpedia 2022: Chapter Four"
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

* Created a ping route (GET /ping) which returns some simple response so that we can easily verify via web whether the service is running.
* Written a cron job that hits this ping endpoint every 15 minutes, and sends out an email to tool maintainers if the server is found to be not running.
* Written a GitHub action that automatically deploys code to toolforge whenever you commit to the main branch (it would ssh into toolforge and run git pull + npm install + webservice restart)
* Build the backend service to verify the source using the unreliable.json file.
* Added the functionality to show Loading... on screen while waiting for a backend call.

      // API to verify source
      app.post('/api/v1/verifySource', async (req, res) => {
        const linkValue = req.body;
      
        const BreakError = {};
        var flag = 0;
        var comment = "";
        var kind = "";
        try{
          var url = new URL(linkValue.linkValue);
          try {
            data.then(function(json){
              try{
              (json).forEach(element => {
                const Origins = element.list;
                var regex = element.regex;
                var re = new RegExp('\\b(?:' + regex + ')\\b');
                if(element.list != null){
                  if (Origins.some(origin => url.origin.includes(origin))) {
                    comment = element.comment;
                    kind = element.kind;
                    flag = 1;
                    res.send({ comment, flag, kind });
                    throw BreakError;
                  }
                }
                if(element.regex!=null){
                  if(re.test(url)){
                    comment = element.comment;
                    kind = element.kind;
                    flag = 1;
                    res.send({ comment, flag, kind });
                    throw BreakError;
                  }
                }
              });
            } catch (err) {
              if (err !== BreakError) throw err;
            }
              if(flag==0){
                res.send({comment, flag, kind});
              }
            });
            
          } 
          catch (error) {
            res.send('failure')
            res.sendStatus(404);
          }
          }
          catch(error){
            flag=2;
            res.send({comment, flag, kind});
          }
         
      })

It was really a great week learning and pushing my backend development skills to a new level by learning a lot of new stuff and integrating with frontend with Node.js.