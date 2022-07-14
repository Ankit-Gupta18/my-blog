+++
categories = ["GSOC"]
date = 2022-06-25T19:32:00Z
description = "Gsoc experience chapter two"
draft = true
image = "/uploads/13-removebg-preview.png"
tags = ["Internship", "GSoC"]
title = "GSoCpedia 2022: Chapter Two"
type = "post"

+++
> “It's not the Destination, It's the journey.”
>
> \~ Ralph Waldo

It’s been less than a month but this community has really grown on me. The past few weeks have been really eventful. A huge shoutout to my mentor, **Daniel Glus, and Siddharth** for giving me the best onboarding experience ever! In this short span, I gained a new sense of professionalism and a clearer view of what it meant to be working as a community! 💜

### Highlights

#### Week 3 - 4(27th June - 10th July)

Of all the past and upcoming weeks, this one is always going to be my favorite. I got to learn about how things actually run behind the front, on the server!! :)

* Changed the citation screen to use Citoid API(extracts the citation from the URL) and display it on the talk page.
* Added functionality to let users know they are on the process of editing while selecting the spot by dimming the background.
* Build the backend server to check if the quote comes from the cited URL.

      // API to verify the quote if it comes from source
      app.post('/api/v1/verifyQuote', async (req, res) => {
        const { linkValue, quoteValue } = req.body;
        try {
          fetch(linkValue)
          .then(res => res.text())
          .then((html) => {
            const { document } = (new JSDOM(html)).window;
            const isParagraphTextOnPage =  document.body.textContent.includes( quoteValue )
            res.send({isParagraphTextOnPage})
          }); 
        } catch (error) {
          console.log(error)
          res.send('failure')
          res.sendStatus(404);
        } 
      })


* Added functionality to store the section(from the article) of the spot where the edit is to be made.
* Learned more about the Wikimedia server named Toolforge.
* Created a Wikimedia developer account and submitted the Toolforge project membership request.
* Discussed the working of the Toolforge with the mentors, and also deployed the production files to the server. Got to learn a lot in this meet about how things actually run behind the front, on the server.

  ![](/uploads/2.png)
* Successfully deployed my project(MVP) on the server!!!

It was really a productive week coding. Learned more about professionalism and how things actually work behind the front. Looking forward for more such productive weeks of coding!!!