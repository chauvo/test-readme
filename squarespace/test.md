## Studio Partnership Program - Studio Owner Registration

Story [727 - As a studio owner I want to be able to register for a CLI Studios account on www.clistudios.com](https://www.pivotaltracker.com/story/show/171913727)


- **Modal**

Put this snippet at the top of SquareSpace page.

```html
<head>
  <meta content="width=device-width, initial-scale=1.0" name="viewport">
</head>
<style>
  .modal {
    opacity: 0;
    transition: opacity 0.5s ease-in-out;
    display: none;
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0%;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgb(0,0,0);
    background-color: rgba(0,0,0,0.4);
  }

  .close {
    text-align: right;
    color: #00bce4;
    font-size: 2em;
    font-weight: 200;
    margin: 5px 20px;
  }

  .close:hover,
  .close:focus {
    text-decoration: none;
    cursor: pointer;
  }

  .modal-content {
    position: relative;
    background-color: white;
    margin: 50px auto 0;
    border: 1px solid #888;
    border-radius: 10px;

    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
    -webkit-animation-name: animatetop;
    -webkit-animation-duration: 0.4s;
    animation-name: animatetop;
    animation-duration: 0.4s
  }

  .studio-owner-registration-form.modal-content {
    width: 830px;
  }

  @-webkit-keyframes animatetop {
    from {top:-300px; opacity:0}
    to {top:0; opacity:1}
  }

  @keyframes animatetop {
    from {top:-300px; opacity:0}
    to {top:0; opacity:1}
  }

  .modal-body {
    -webkit-overflow-scrolling: touch;
    padding: 5px;
  }

  .register-button {
    font-family: Oxygen;
    font-size: 15px;
    font-weight: 700;
    font-style: normal;
    text-transform: uppercase;
    letter-spacing: .1em;
    color: #fff;
    background-color: #00bee3;
    height: 50px;
    padding: 10px 30px;
    cursor: pointer;
    outline: none;
    border: none;
  }

  .register-button:hover {
    opacity: 0.8;
  }

  #studioOwnerSignUpIframeProduction {
    width: 100%;
  }

  @media only screen and (max-width: 830px) {
    .studio-owner-registration-form .close {
      margin-top: 0;
      padding-top: 10px;
    }

    .studio-owner-registration-form.modal-content {
      width: 100%;
      height: 100%;
      margin-top: 0;
      border-radius: 0;
      border: none;
    }

    .studio-owner-registration-form .modal-body {
      height: 100%;
      padding: 0;
    }
  }
</style>

<div id="studioOwnerRegisterModal" class="modal">
  <div class="studio-owner-registration-form modal-content">
    <div class="close">×</div>
    <div class="modal-body">
      <iframe src="https://members.clistudios.com/studio_owners/sign_up" frameborder="0" id="studioOwnerSignUpIframeProduction" scrolling="no"></iframe>
    </div>
  </div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function(event) {
    var modal = document.getElementById('studioOwnerRegisterModal');
    var closeBtn = document.getElementsByClassName("close")[0];
    var iframe = document.getElementById('studioOwnerSignUpIframeProduction');

    closeBtn.onclick = function() {
      modal.style.display = "none";
    }

    window.onkeydown = function(event) {
      event = event || window.event;
      if (event.keyCode == 27) {
        modal.style.display = "none";
      }
    };

    window.addEventListener('message', function (event) {
      if (event.data.hasOwnProperty('studioOwnerFrameHeight')) {
        //Set height of the Iframe
        iframe.height = (event.data.studioOwnerFrameHeight) + "px";
        modal.style.opacity = 1;
      }
      if (event.data.hasOwnProperty('studioOwnerSignUpSuccessfully')) {
        window.location.href = event.data.studioOwnerSignUpSuccessfully
      }
      if (event.data.hasOwnProperty('studioOwnerSignInUrl')) {
        window.location.href = event.data.studioOwnerSignInUrl
      }
    });
  });
</script>
```


- **Button**

Put this snippet at anywhere of the SquareSpace page above that you want to show the button.

Remember changing the button id if you have more than 1 button in a page.

```html
<!-- NEED TO EDIT -->

<button id="registerButtonProduction" class="register-button" disabled>Join Today →</button>

<script type="text/javascript">
  document.addEventListener("DOMContentLoaded", function(event) {
    var btn = document.getElementById("registerButtonProduction");
    var modal = document.getElementById('studioOwnerRegisterModal');
    var iframe = document.getElementById('studioOwnerSignUpIframeProduction');

    btn.onclick = function() {
      modal.style.display = "block";
      iframe.contentWindow.postMessage('studioOwnerFrameHeight', "*");
    }

    window.addEventListener('message', function (event) {
      if (event.data == 'studioOwnerIframeDidLoad') {
        btn.disabled = false
      }
    });
  });
</script>
```
