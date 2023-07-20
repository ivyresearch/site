---
title: "How to Enable SXG"
date: 2023-06-24T15:58:00-06:00
draft: false
---

Here are some steps to move a site deployed on Render.com to enable Signed HTTP Exchanges (SXG):

- Build your site locally with SXG enabled. This involves generating a .well-known/signed-exchange.json file and signing your content using a private key. There are libraries like sxg-js that can help with this.
- Push your built site to a new Git repository. Render allows connecting to GitHub, GitLab, or Bitbucket repositories.
- Create a new Web Service on Render.com and link it to the new SXG-enabled Git repository.
- Configure the Web Service's Environment Variables to specify your certificate and private key for signing content. Render allows setting secure environment variables.
- Deploy the new Web Service on Render. This will pull your SXG-enabled build from the linked Git repo.
- Update your DNS records to point your domain to Render's servers IP addresses. This will route traffic to your new SXG-enabled Render deployment.
- Add any required SXG certificates to your domain. This allows browsers to verify signed exchanges.
- Configure your server for SXG delivery, such as setting the correct Content-Type headers.
- Test that you can fetch signed exchanges for your site by accessing .well-known/signed-exchange.json.
- That covers the key steps! Let me know if you have any other questions. Migrating to SXG can improve performance and security for your Render-hosted site.

## Let's dynamically fetch content from our API.

What you're currently reading is typical Hugo content authored in Markdown. Below the break we see content loaded dynamically via HTMX from our API server.

Open `content/posts/hello-world.md` to follow along with the code.

---

{{< htmx.inline >}}
<div
  hx-get="{{ .Site.Params.apiBaseUrl }}/hello_world"
  hx-trigger="load"
  hx-vals='js:{"name": new URLSearchParams(window.location.search).get("name")}'
  hx-on="htmx:configRequest: console.log('detail:', event.detail); event.detail.headers='';" />
  <p>Content loading from API...</p>
</div>
{{< /htmx.inline >}}

---

## Let's add a form

Writing markdown content is great, but sometimes you want to add hypermedia controls: buttons, forms, etc.

See `func helloWorldForm` from `server.go` to see what's going on behind the scenes with this form.

Here we are using a Hugo concept called an "inline shortcode". This allows us to change the base URL for our API server, depending on whether we're in development or production.


{{< htmx.inline >}}
<!-- Make sure the api base URL is set -->
<form hx-post="{{ .Site.Params.apiBaseUrl }}/hello_world_form">
  <label>Name</label>
  <input type="text" name="name">
  <br/>
  <button>Submit</button>
</form>
{{< /htmx.inline >}}


---

## Let's add a simple button that loads content

{{< htmx.inline >}}
<div
  hx-get="/content.html"
  hx-trigger="click" />
  <button>Load content</button>
</div>
{{< /htmx.inline >}}


