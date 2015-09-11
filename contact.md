---
layout: default
title: Contact Us
shortsummary: We are open to new opportunities and will be glad to answer your questions. Please cotact us. 
---

<script>
function sendEmail(fromemail, fromname, subject, body, toemail, toname) {
  console.log("Sending email. from:" + fromemail + " to:" + toemail + "(" + toname + ") subject:" + subject + " body:" + body);
  $.ajax({
    type: 'POST',
    url: 'https://mandrillapp.com/api/1.0/messages/send.json',
    data: {
      'key': 'yivmuojtNKW7KLSb2NeHhg',
      'message': {
        'from_email': fromemail,
        'to': [
            {
              'email': toemail,
              'name': toname,
              'type': 'to'
            }
          ],
        'autotext': 'true',
        'subject': "WeSolveProblems Message: " + subject,
        'html': "New message on the WeSolveProblems website" + 
                "<br>From: " + fromname + " (" + fromemail + ")" +   
                "<br>Subject: " + subject +  
                "<br>=====================================" + 
                "<br><pre>" + body + "</pre>"
      }
    }
   }).done(function(response) {
     console.log(response); // if you're into that sorta thing
 });
}

function handleSendEmail(event) {
  var fromname = $("#inputYourName").val();
  var fromemail = $("#inputYourEmail").val();
  var subject = $("#inputSubject").val();
  var body = $("#inputBody").val();
  var atsymbol = "@";
  sendEmail(fromemail, fromname, subject, body, "vassiliphilippov" + atsymbol + "gmail.com", "Vassili Philippov");
  sendEmail(fromemail, fromname, subject, body, "elena.boguslavskaya" + atsymbol + "brunel.ac.uk", "Elena Boguslavskaya");
  alert("Your message is sent. Thank you! We will contact you soon.");
  event.preventDefault();
}
</script>

<form action="#" id="contact-form">
  <div class="form-group" action="#">
    <label for="inputYourName">Your name</label>
    <input type="text" class="form-control" id="inputYourName" placeholder="Name">
  </div>
  <div class="form-group">
    <label for="inputYourEmail">Your email</label>
    <input type="email" class="form-control" id="inputYourEmail" placeholder="Email">
  </div>
  <div class="form-group">
    <label for="inputSubject">Subject</label>
    <input type="text" class="form-control" id="inputSubject" placeholder="Subject">
  </div>
  <div class="form-group">
    <label for="inputBody">Message</label>
    <textarea class="form-control" rows="12" id="inputBody"></textarea>
  </div>
  <div class="form-group">
    <button type="submit" class="btn btn-primary btn-large" id="button-send">Send</button>
  </div>
</form>

<script>
//$(document).ready(function () {
  $("#contact-form").one('submit', function(event) {
    handleSendEmail(event);
  });
//  $("#button-send").click(sendEmail);
//});
</script>
