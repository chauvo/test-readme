Squarespace

```javascript
const xhr = new XMLHttpRequest();
const internationalLandingPage = 'https://members.clistudios.com/international';
const ipValidatorUrl = 'https://08635360.ngrok.io/api/v1/ip_validators';
xhr.open('GET', ipValidatorUrl, false);
xhr.send();
if(xhr.status === 200) {
   var response = JSON.parse(xhr.responseText);
   if (response.international_ip) {
     window.location.href = 'https://members.clistudios.com/international'
   }
}
```
