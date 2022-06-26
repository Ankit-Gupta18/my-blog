+++
categories = ["GSOC"]
date = 2022-06-25T19:32:00Z
description = "Gsoc experience chapter one"
image = "/uploads/12-removebg-preview.png"
tags = ["Internship", "GSoC"]
title = "GSoCpedia 2022: Chapter One"
type = "post"

+++
> _“The mission of the Wikimedia Foundation is to empower and engage people around the world to collect and develop educational content under a free license or in the public domain, and to disseminate it effectively and globally.”_

### Getting started

The project I will be working on is the [Edit Request Wizard](https://summerofcode.withgoogle.com/programs/2022/projects/u0WNs8PY "Project").  This project aims at creating a step-by-step form to help beginners submit a Wikipedia edit request. An edit request is a request for someone to change some text in an article. Edit requests are an important part of Wikipedia. The form created in this project will help the edit requests comply with Wikipedia policy. It will be developed as a Wikipedia user script that shows a form for submitting a Wikipedia edit request, with high-quality guidance and error messages, suitable for use by beginners, and a backend server that the user script will make calls to for validation of source and quote.

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