<h1 align="center">
  <br>
  📩 A Template to host an MTA-STS Policy file on GitHub
  <br>
</h1>

<h4 align="center">Use this template to host your <i>MTA Strict Transport Security (MTA-STS)</i> <a href="https://datatracker.ietf.org/doc/html/rfc8461">[RFC 8461]</a> policy file on GitHub Pages.</h4>

<p align="center">
  <a href="#how-to-use">How To Use</a> •
  <a href="#license">License</a> •
  <a href="#author">Author</a>
</p>

MTA-STS is a security standard to secure e-mail delivery. E-mail servers that send inbound e-mail to your domain will be able to detect that your e-mail server supports SMTP-over-TLS via `STARTTLS` (also known as [Opportunistic TLS](https://en.wikipedia.org/wiki/Opportunistic_TLS)) before opening the actual connection.

In case the sending e-mail server is not able to initiate a secure connection, it will end the connection to enforce transport layer encryption. This mitigates [Man-in-the-middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) DNS and SMTP [downgrade attacks](https://en.wikipedia.org/wiki/Downgrade_attack) that would allow an attacker to read or manipulate e-mail in transit.

## How To Use

1. Make sure you are [signed in to GitHub](https://github.com/login). Then click on [**Use this template**](https://github.com/jpawlowski/mta-sts.template/generate) to create a copy to your own GitHub profile (see [GitHub Docs](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)). Don't _clone_ the repository.
   You may name your repository whatever you like. For simplicity, you can name it `mta-sts.<your_domain.tld>`.

2. Change the file `.well-known/mta-sts.txt` according to your needs.

3. Create a `CNAME` record for `mta-sts.<your_domain.tld>` in your domain's DNS that points to `<user>.github.io` or `<organization>.github.io` and [enable GitHub Pages](https://docs.github.com/articles/using-a-custom-domain-with-github-pages/).

4. Open a browser to `https://mta-sts.<your_domain.tld>` and make sure it does not show any certificate warnings.

5. Create a `TXT` record for `_mta-sts.<your_domain.tld>` in your domain's DNS to enable the MTA-STS policy for your domain.
   You may copy & paste this to your DNS provider:

   ```dns
   #HOST       #TTL    #TYPE    #VALUE
   _mta-sts    3600    TXT      "v=STSv1; id=20220317000000Z"
   ```

   Note that you will need to change the `id=` here whenever you make changes to your `mta-sts.txt` policy file.

6. Validate your setup, for example by using the [MTA-STS validator](https://aykevl.nl/apps/mta-sts/) created by [@aykevl](https://github.com/aykevl/mta-sts).

*Optional (but __highly recommended__):*

7. Create another `TXT` record for `_smtp._tls.<your_domain.tld>` in your domain's DNS to enable reporting (see [RFC 8460](https://datatracker.ietf.org/doc/html/rfc8460)).
   You may copy & paste this to your DNS provider:

   ```dns
   #HOST         #TTL    #TYPE    #VALUE
   _smtp._tls    3600    TXT      "v=TLSRPTv1; rua=mailto:tls-rua@mailcheck.<your_domain.tld>"
   ```

   Note that the e-mail recipient mailbox shall be on a different domain _without_ MTA-STS being configured.
   It is also quite painful to manually deal with the reports other e-mail providers will send to you. For that particular reason, you may want to consider sending these e-mails to a 3rd-party tool like [Report URI](https://report-uri.com/), [URIports](https://www.uriports.com/), or from other commercial providers.
   
   You probably want this to be the same tool you might use for DMARC reports, like [DMARC Analyzer](https://www.dmarcanalyzer.com/) or [Dmarcian](https://dmarcian.com/).

## License

[MIT License](https://github.com/jpawlowski/mta-sts.template/blob/gh-pages/LICENSE)

## Author

[julian.pawlowski.me](https://julian.pawlowski.me/) &nbsp;&middot;&nbsp;
GitHub [@jpawlowski](https://github.com/jpawlowski/mta-sts.template) &nbsp;&middot;&nbsp;
Twitter [@Loredo](https://twitter.com/Loredo)
