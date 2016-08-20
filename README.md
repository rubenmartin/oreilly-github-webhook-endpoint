Demo GitHub API-based Service
=============================

This is a demo webhook endpoint (server) for chapter A4 of the [Mastering Advanced GitHub](#FIXME) video series at O’Reilly, focusing on the GitHub API.

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)
[![Dependency Status](https://gemnasium.com/deliciousinsights/oreilly-github-webhook-endpoint.svg)](https://gemnasium.com/deliciousinsights/oreilly-github-webhook-endpoint)


Usage
-----

  1. Make sure you have [Node.js installed](https://nodejs.org/en/download/)
  2. Clone this repo
  3. Open a Terminal and `cd` into the clone's directory
  4. Run `npm install` to get the (few) dependencies
  5. Run `npm start` to run the server

This will run the server on **port 45678, or the nearest higher available port** of your machine.  It will look something like this:

```text
> webhook-endpoint@1.0.0 start …/oreilly-github-webhook-endpoint
> node server.js

GitHub App credentials properly loaded. Checking them…
Demo service listening on http://localhost:45678/
Webhook secret token for this run is e31ea528972adc5034492f44eae6870a06c6c8ed8a3601c61af188578b1b1069

Just hit Ctrl+C to stop this server.

[!] Don’t forget to launch an ngrok session: ngrok http 45678
\o/ GitHub App credentials seem to successfully authenticate.
```

But this is just on your machine, and you need GitHub’s servers to be able to access it.  For this, you need some sort of tunnel that connects some network port and address visible to the internet to your own machine and port.  One of the easiest ways to accomplish that across environments and setups is **[ngrok](https://ngrok.com/)**.

  1. [Download](https://ngrok.com/download) ngrok
  2. Make a note of the port your webhook endpoint ran on; for these instructions, we'll assume it was `45678`
  3. Open another Terminal window, and run `ngrok http <the-port>`, for instance `ngrok http 45678`.

This will clear the window and run an ngrok client on your machine, acting as a sort of reverse-proxy so the internet can access your server, both over HTTPS and HTTP.  After a second or two, you should see something that looks like this:

```text
Tunnel Status                 online
Version                       2.0.19/2.0.19
Web Interface                 127.0.0.1:4040
Forwarding                    http://1420f0d6.ngrok.com -> localhost:45678
Forwarding                    https://1420f0d6.ngrok.com -> localhost:45678

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

Until you stop ngrok by hitting <kbd>Ctrl+C</kbd>, you've got your tunnel running.  You can now configure your Webhook to use the public URL based off `ngrok.com`, and this webhook server will dump the JSON payloads GitHub sends into its own Terminal console.

Full annotated source
---------------------

The full annotated source for this is [available online](http://deliciousinsights.github.io/oreilly-github-webhook-endpoint/).

License
-------

This repo © 2016 Christophe Porteneuve & Delicious Insights, and is [MIT licensed](/LICENSE).
