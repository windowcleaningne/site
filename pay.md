---
title: Pay My Bill
layout: page
permalink: /pay
callouts: banner_callouts
hero_height: is-small
hero_image: assets/logo.png
---

<script src="https://js.stripe.com/v3/"></script>
  <script>
    var stripe = Stripe('pk_live_baBiUjoxfXq7Ocq997wqlQ01');
</script>

# Pay My Bill

Please ensure your reference number is accurate. You should have received this through your letterbox or via email.

Completing the form will redirect you to our payment processor. Your credit card details will be required on the next step.

If you are unsure of your reference number, please [contact us](contact-us). All fields are required.


<div class="field">
  <label class="label">Reference Number*</label>
  <div class="control">
    <input id="referenceNo" class="input" type="text" required>
  </div>
</div>

<div class="field">
  <label class="label">Amount*</label>
  <div class="control">
    <input id="amount" class="input" type="number" required>
  </div>
</div>

<div class="field">
  <div class="control">
    <button id="submit" class="button is-link">Pay Securely Now</button>
  </div>
</div>

<script>
document.getElementById('submit').addEventListener('click', function(event) {
  
  // Set Session ID
  var sessionID = "";

  var xmlHttp = new XMLHttpRequest();
    var reference = document.getElementById('referenceNo').value;
    var amount = document.getElementById('amount').value;

    xmlHttp.onreadystatechange = function() {
        if (xmlHttp.readyState == XMLHttpRequest.DONE && xmlHttp.status == 200)
            sessionID = xmlHttp.responseText;
    }
    xmlHttp.open("POST", "https://cjh02f4cue.execute-api.eu-west-1.amazonaws.com/default/wcnePaymentForm", false); // true for asynchronous
    xmlHttp.send(JSON.stringify({ "reference": reference, "amount": amount }));
  
  // Now go to checkout.
  stripe.redirectToCheckout({
    sessionId: sessionID
  }).then(function (result) {
  console.log(result.error.message);
  });
});
</script>
