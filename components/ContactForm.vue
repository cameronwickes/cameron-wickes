<template>
  <form name="ContactForm" method="POST" Content-Type="application/x-www-form-urlencoded" netlify>
    <!-- Name -->
    <div class="field">
      <label class="label is-medium">Name</label>
      <div class="control has-icons-left">
        <input name="Name"class="input is-medium" type="text" placeholder="Full Name" required/>
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
          required
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
          required
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
          required
        ></textarea>
         <span class="icon is-small is-left">
          <font-awesome-icon icon="comment" />
        </span>
      </div>
    </div>
    <br>
    <div class="control">
      <button class="button is-primary is-center" type="submit">
        Contact Me
      </button>
    </div>
  </form>
</template>
