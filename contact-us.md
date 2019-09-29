---
title: Contact Us
layout: page
permalink: /contact-us
callouts: banner_callouts
hero_height: is-small
hero_image: assets/logo.png
---

# Contact Us

<div class="field">
  <label class="label">Name*</label>
  <div class="control">
    <input id="name" class="input" type="text" required>
  </div>
</div>

<div class="field">
  <label class="label">Phone Number*</label>
  <div class="control">
    <input id="phone_number" class="input" type="number" required>
  </div>
</div>

<div class="field">
  <label class="label">Email*</label>
  <div class="control">
    <input id="email" class="input" type="email" required>
  </div>
</div>

<div class="field">
  <label class="label">Address Line 1*</label>
  <div class="control">
    <input id="addrline1" class="input" type="text" required>
  </div>
</div>

<div class="field">
  <label class="label">Address Line 2</label>
  <div class="control">
    <input id="addrline2" class="input" type="text">
  </div>
</div>

<div class="field">
  <label class="label">Postcode*</label>
  <div class="control">
    <input id="postcode" class="input" type="text" required>
  </div>
</div>

<div class="field">
  <label class="label">Type of Clean*</label>
  <div class="control">
    <div class="select">
      <select id="type_of_clean">
        <option>Regular Clean</option>
        <option>One-Off Clean</option>
      </select>
    </div>
  </div>
</div>

<div class="field">
  <label class="label">Number of Bedrooms*</label>
  <div class="control">
    <div class="select">
      <select id="bedrooms">
        <option selected>1</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5+</option>
        <option>Other</option>
        <option>Commercial</option>
      </select>
    </div>
  </div>
</div>

<div class="field">
  <label class="label">Message</label>
  <div class="control">
    <textarea id="message" class="textarea">My Message...</textarea>
  </div>
</div>

<div class="field">
  <div class="control">
    <button id="submit" class="button is-link">Submit Enquiry</button>
  </div>
</div>

<!-- Hidden by default. Form submit unhides. Close button re-hides -->
<div class="notification is-success hidden" id="submit-notification">
  <button class="delete" id="submit-delete"></button>
  Thanks. Your enquiry has been sent. We'll be in touch soon.
</div>

<script>
  // Form submit clicked...
  document.getElementById('submit').addEventListener('click', function(event) {

    // Prevent form submission default, disable the submit button and show the notification.
    event.preventDefault();
    document.getElementById('submit').disabled = true;
    document.getElementById('submit-notification').classList.remove("hidden");

    name = document.getElementById('name').value;
    phone_number = document.getElementById('phone_number').value;
    email = document.getElementById('email').value;
    addrline1 = document.getElementById('addrline1').value;
    addrline2 = document.getElementById('addrline2').value;
    postcode = document.getElementById('postcode').value;
    type_of_clean = document.getElementById('type_of_clean').value;
    bedrooms = document.getElementById('bedrooms').value;
    message = document.getElementById('message').value;

    // Submit data to AWS API
    var xmlhttp = new XMLHttpRequest();
    var theUrl = "https://ao4ui2rs2l.execute-api.eu-west-1.amazonaws.com/default/sendWCNEContactFormEmail";
    xmlhttp.open("POST", theUrl);
    xmlhttp.send(JSON.stringify({ "name": name, "phone_number": phone_number, "email": email, "addr1": addrline1, "addr2": addrline2, "postcode": postcode, "type_of_clean": type_of_clean, "bedrooms": bedrooms, "message": message}));

  });

  // When notification delete button is clicked, hide notifiction.
  document.getElementById('submit-delete').addEventListener('click', function(event) {
    document.getElementById('submit-notification').classList.add("hidden");
  });
</script>
<style>
.hidden {
  visibility: hidden;
}
</script>

