<template>
  <form name="ContactForm" action="/success" method="POST" netlify-honeypot="bot-field" data-netlify="true">
    <p class="hidden">
    <label>Don’t fill this out if you're human: <input name="bot-field" /></label>
    </p>
    <!-- Name -->
    <div class="field">
      <label class="label is-medium">Name</label>
      <div class="control has-icons-left">
        <input name="Name"class="input is-medium" type="text" placeholder="Full Name" />
        <span class="icon is-small is-left">
          <font-awesome-icon icon="user" />
        </span>
      </div>
    </div>
    <!-- Email -->
    <div class="field">
      <label class="label is-medium">Email</label>
      <div class="control has-icons-left">
        <input
          name="Email"
          class="input is-medium"
          type="email"
          placeholder="Email Address"
        />
        <span class="icon is-small is-left">
          <font-awesome-icon icon="envelope" />
        </span>
      </div>
    </div>
    <!-- Subject -->
    <div class="field">
      <label class="label is-medium">Subject</label>
      <div class="control has-icons-left">
        <input
          name="Subject"
          class="input is-medium"
          type="text"
          placeholder="Summary"
        />
        <span class="icon is-small is-left">
          <font-awesome-icon icon="briefcase" />
        </span>
      </div>
    </div>
    <!-- Message -->
    <div class="field">
      <label class="label is-medium">Message</label>
      <div class="control has-icons-left">
        <textarea
          name="Message"
          class="textarea is-medium"
          placeholder="Detailed description of your comment, request, etc"
          rows="8"
        ></textarea>
         <span class="icon is-small is-left">
          <font-awesome-icon icon="comment" />
        </span>
      </div>
    </div>
    <div class="control">
      <button class="button is-primary is-center" type="submit">
        Contact Me
      </button>
    </div>
  </form>
</template>
