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

#### Week 1 - 2(13th - 26th June)

* Discussed the project idea on Minimum Viable Product(MVP), and the overall workflow of the project with mentors in the meeting.

  ![](/uploads/gsoc-meet-1.png)
* Learned OOUI for creating the user interface of the form and MediaWiki API to add functionality in the form to make API calls.
* Created the initial frontend ie an edit request form shown as a popup with the following steps:
  * Input for the URL
  * An interface to select the location of the text
  * Input for the Quote
  * Input for the Rephrased Quote

  ![](/uploads/form-blog-chapter-one.png)
* Added functionality to the form to put these values on the Talk Page of the current article using MediaWiki API calls.

      function editPage( info ) {
            var api = new mw.Api();
            api.postWithToken("csrf", {
              action: 'edit',
              title: info.title,
              appendtext: info.text, // will replace entire page content
              summary: info.summary
            } ).done(function( data ) {
              alert( 'Edit Request sent to talk page..!' );
            } ).fail( function(code, data) {
              console.log( api.getErrorMessage( data ).text());
            } );
          }
          // API calls code goes here
                  editPage({
                    title: (new mw.Title(mw.config.get("wgPageName"))).getTalkPage().toText(),
                    text: '<b>Edit Request made by</b> ~~' + '~~' + '<br><b>Source URL:</b> ' + linkValue + '<br><b>Spot where to add the fact:</b> ' + selectValue + '<br><b>Quote:</b> ' + quoteValue + '<br><b>Rephrased Quote:</b> ' + requoteValue + '<br><br> ',
                    summary: 'Edit Request to add a fact'
                  }); 

  ![](/uploads/talk-page-interface-blog-chapter-one.png)

  It was great week coding on the MVP. Learned many new tech stacks and had a great learning experience. In the coming weeks, I might be working more on the UI enhancement and adding more functionalities to my form.