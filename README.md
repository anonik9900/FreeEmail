# :pencil: Free Open-Source Mini Email Client

http://freeemail.altervista.org/

-------------------------------------------------------------------------------------------------------------------------------------


<div align ="center">
   <img src="http://freeemail.altervista.org/logo.png" alt="" width="100" height="100">
  <br>
   <h1>Free Email Sender</h1>
   <br>
   <p>
      Free Open-Source Mini Email Client 
      Written in Html5,Css,Php And JavaScript
   </p>
<p>
  How to use in your 2nd Website page ? 
  Use this code<br>
   <h2>HTML Code</h2>
   <pre>
   
<!DOCTYPE html>
<html>
  <head>
    <title>Free Email Sender</title>
    <link rel="icon" src="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, minimal-ui">
    <link rel="stylesheet" href="app.min.css">
    <style>
			@-webkit-keyframes pulse {
				0% {
					background-color: #CCC;
				}
				25% {
					background-color: #EEE;
				}
				50% {
					background-color: #CCC;
				}
				75% {
					background-color: #EEE;
				}
				100% {
					background-color: #CCC;
				}
			}

    </style>

 <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0-beta/css/materialize.min.css">

  </head>

  <body>
    <div class="app-page" data-page="home">
      <div align ="center">
      <img src="logo.png" alt="" width="100" height="100">
    </div>
      <div class="app-topbar blue">
        <div class="app-title">Invia Email</div>
      </div>
      <div class="app-content">
          <p class="app-section">
					Clicca il pulsante per inviare un Email
				</p>


          <div class="app-section" id="contact-list">

				</div>

        <div class="app-section">
          <div align ="center">
          <div class="app-button waves-effect waves-light btn" id="new-user">Invia a nuovo utente</div>
        </div>
        </div>

      </div>
    </div>
<a href="en.html">English Page</a>
  <div class="app-page" data-page="sendemail">
			<div class="app-topbar">
				<div class="app-title"><span class="app-icon"></span>Invia Email</div>
				<div class="right app-button" data-back>Esci X</div>
			</div>

			<div class="app-content">

                <div class="app-section" id="message">

				</div>

				<div class="app-section">
					Da: <input class="app-input" id="sender-email" placeholder="Indirizzo Email con cui stai inviando questo messaggio">
				</div>

                <div class="app-section">
					A: <input class="app-input" id="recipient-email" placeholder="Indirizzo Email Destinatario">
				</div>

				<form class="app-section">
					<input class="app-input" name="subject" placeholder="Oggetto" id="subject">
					<textarea class="app-input" name="message" placeholder="Messaggio" id="content"></textarea>
					<div class="app-button green app-submit" id="send-button">Invia</div>
				</form>
			</div>
		</div>

    <script src="zepto.js"></script>
    <script src="app.min.js"></script>
    <script>

      App.controller('home', function (page) {

          if (typeof localStorage !== 'undefined') {

              $(page).find("#new-user")
                .clickable()
                .click(function () {

                  if (localStorage.getItem("recipient-email") !== null) {

                      localStorage.removeItem("recipient-email");


                  }

                  App.load("sendemail");

              })

              if (localStorage.getItem("recipient-list") !== null) {

                  var recipientList = JSON.parse(localStorage.getItem("recipient-list"));

                  $.each(recipientList, function( index, value ) {

                      $(page).find("#contact-list").append('<div class="app-button redirect">' + value + '</div>');

                  });

                  $(page).find("#contact-list").show();

                  $(page).find(".redirect")
                      .clickable()
                      .on("click", function() {

                      localStorage.setItem("recipient-email", $(this).html());

                      App.load('sendemail');



                  });


              } else {

                  $(page).find("#contact-list").hide();

              }


          }

      });

        App.controller('sendemail', function (page) {

            $(page).find("#message").hide();

            if (typeof localStorage !== 'undefined') {

                if (localStorage.getItem("sender-email") !== null) {


                    $(page).find("#sender-email").val(localStorage.getItem("sender-email"));

                }

                if (localStorage.getItem("recipient-email") !== null) {

                    $(page).find("#recipient-email").val(localStorage.getItem("recipient-email"));

                }

            }



          $(page).find('#send-button')
					.clickable()
					.on('click', function () {

                 $.ajax({
  type: 'GET',
  url: 'http://completewebdevelopercourse.com/content/9-mobileapps/sendemail.php?callback=response',
  // data to be added to query string:
  data: { to: $("#recipient-email").val(), from: $("#sender-email").val(), subject: $("#subject").val(), content: $("#content").val()},
  // type of data we are expecting in return:
  dataType: 'jsonp',
  timeout: 300,
  context: $('body'),
  success: function(data){

      if (data.success == true) {

          $(page).find("#message").html("Your email was sent successfully!").show();

      } else {

          $(page).find("#message").html("Your email could not be sent - please try again later.").show();

      }


  },
  error: function(xhr, type){

        $(page).find("#message").html("Your email could not be sent - please try again later.").show();

  }
})


              if (typeof localStorage !== 'undefined') {

                  localStorage.setItem("sender-email", $("#sender-email").val());

                  var recipientList = new Array();

                  if (localStorage.getItem("recipient-list") !== null) {

                      recipientList = JSON.parse(localStorage.getItem("recipient-list"));

                  }

                  if ($.inArray($("#recipient-email").val(), recipientList) == -1) {

                      recipientList.push($("#recipient-email").val());

                      recipientList.sort();

                      localStorage.setItem("recipient-list", JSON.stringify(recipientList));

                      console.log(recipientList);

                  }

              } else {

                  // alert user that we couldn't save data

              }


          });
      });



      try {
        App.restore();
      } catch (err) {
        App.load('home');
      }
    </script>
  </body>
</html>
</pre>
