---
layout: page
title: Meteor Security Checklist
class: checklist
---

## Dependencies

<p class="todo-item"><i data-feather="check-square"></i> Use Package Scan to check for Meteor packages with known vulnerabilities.</p>

Your application code may be secure, but if you’re using a vulnerable Meteor package, your application is vulnerable.

<i data-feather="link"></i> [https://github.com/east5th/package-scan](https://github.com/East5th/package-scan)

<p class="todo-item"><i data-feather="check-square"></i> Use Snyk and/or NSP to check for Node.js packages with known vulnerabilities.</p>

Node.js dependencies lay the foundation for your Meteor application. Make sure that your foundation is sound.

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/06/20/node-vulnerability-scanners-in-a-13-world/](http://www.east5th.co/blog/2016/06/20/node-vulnerability-scanners-in-a-13-world/)

## Methods, Publications, and Server-side Routes

<p class="todo-item"><i data-feather="check-square"></i> Thoroughly check <em>all</em> method, publication, and route arguments.</p>

Using `check` to make assertions about the type and shape of user inputs can prevent entire families of NoSQL injection vulnerabilities.

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/03/21/nosql-injection-in-modern-web-applications/](http://www.east5th.co/blog/2016/03/21/nosql-injection-in-modern-web-applications/)

<i data-feather="link"></i> [https://github.com/East5th/check-checker](https://github.com/East5th/check-checker)

<p class="todo-item"><i data-feather="check-square"></i> Use trusted fields (like <code class="highlighter-rogue">this.userId</code>) whenever possible.</p>

Never use a user-provided field when a trusted alternative is available.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#user-id-client](https://guide.meteor.com/security.html#user-id-client)

<p class="todo-item"><i data-feather="check-square"></i> Verify that methods, publications, and server-side routes are making authentication and authorization checks.</p>

Always verify that the current user has permission to do the thing they’re trying to do. Similarly, never assume that an unauthorized user can’t call a method or publication because it wasn’t publicly defined.

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/02/01/sending-emails-through-hidden-methods/](http://www.east5th.co/blog/2016/02/01/sending-emails-through-hidden-methods/)

<p class="todo-item"><i data-feather="check-square"></i> Always be aware of where your code is running.</p>

In a Javascript-everywhere ecosystem, we can sometimes forget whether a specific piece of code runs of the client or the server.

<i data-feather="link"></i> [http://www.east5th.co/blog/2015/09/21/never-forget-where-your-code-runs/](http://www.east5th.co/blog/2015/09/21/never-forget-where-your-code-runs/)

<p class="todo-item"><i data-feather="check-square"></i> Test that MongoDB queries are behaving as expected in all circumstances.</p>

Incorrectly written queries can lead to over-publishing and the leaking of data to the client.

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/09/05/querying-non-existent-mongodb-fields/](http://www.east5th.co/blog/2016/09/05/querying-non-existent-mongodb-fields/)

<p class="todo-item"><i data-feather="check-square"></i> Rate limit and unblock your methods and publications where appropriate.</p>

Take basic precautions against attackers potentially carrying out Denial of Services attacks through excessive method calls or subscriptions.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#rate-limiting](https://guide.meteor.com/security.html#rate-limiting)

<p class="todo-item"><i data-feather="check-square"></i> Avoid allow & deny collection validators.</p>

Allow and deny rules can be hard to reason about and even harder to implement correctly.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#allow-deny](https://guide.meteor.com/security.html#allow-deny)

<i data-feather="link"></i> [http://www.east5th.co/blog/2015/06/15/allow-and-deny-challenge-check-yourself/](http://www.east5th.co/blog/2015/06/15/allow-and-deny-challenge-check-yourself/)

<p class="todo-item"><i data-feather="check-square"></i> Always whitelist the fields of documents returned by methods and especially subscriptions.</p>

Whitelisting the fields returned by a query can prevent sensitive data being accidentally leaked to the client.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#fields](https://guide.meteor.com/security.html#fields)

<p class="todo-item"><i data-feather="check-square"></i> Use reactive data sources to securely invalidate cursors returned by publications.</p>

Use reactive data sources like `this.userId`, or `peerlibrary:reactive-publish` to continually ensure that a user is authorized to see the data being published.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#publications-user-id](https://guide.meteor.com/security.html#publications-user-id)

<i data-feather="link"></i> [https://github.com/peerlibrary/meteor-reactive-publish](https://github.com/peerlibrary/meteor-reactive-publish)

## Front-end

<p class="todo-item"><i data-feather="check-square"></i> Limit and audit the use of raw HTML injection.</p>

Triple braces in Blaze and `dangerouslySetInnerHTML` in React should be used sparingly. User-provided data being injected directly into the DOM should be thoroughly sanitized.

<i data-feather="link"></i> [http://www.east5th.co/blog/2015/04/03/black-box-meteor-triple-brace-xss/](http://www.east5th.co/blog/2015/04/03/black-box-meteor-triple-brace-xss/)

<i data-feather="link"></i> [http://www.east5th.co/blog/2015/09/07/hijacking-meteor-accounts-with-xss/](http://www.east5th.co/blog/2015/09/07/hijacking-meteor-accounts-with-xss/)

<p class="todo-item"><i data-feather="check-square"></i> Check for other instances of cross-site scripting vulnerabilities.</p>

Third party packages and plugins can sometimes be vulnerable to cross-site scripting attacks. Make sure you’re sanitizing user-provided data before handing it off to any front-end library.

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/03/14/stored-xss-and-unexpected-unsafe-eval/](http://www.east5th.co/blog/2016/03/14/stored-xss-and-unexpected-unsafe-eval/)

<p class="todo-item"><i data-feather="check-square"></i> Tighten up your content security policy.</p>

Use the `browser-policy` Meteor package to add a Content Security Policy to your application. Fine tune the CSP to meet your application’s needs.



## Infrastructure

<p class="todo-item"><i data-feather="check-square"></i> Always use TLS/SSL.</p>

Use `force-ssl` or configure your load balancer/reverse proxy to always redirect clients to a secure connection.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#ssl](https://guide.meteor.com/security.html#ssl)

<p class="todo-item"><i data-feather="check-square"></i> Consider rate limiting static asset and <code class="highlighter-rogue">/websocket</code> requests.</p>

Upfront work can mitigate the pain of Denial of Service attacks in the future.

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/05/16/the-missing-link-in-meteors-rate-limiter/](http://www.east5th.co/blog/2016/05/16/the-missing-link-in-meteors-rate-limiter/)

<p class="todo-item"><i data-feather="check-square"></i> Ensure no sensitive business secrets are being bundled with the client Javascript application.</p>

Malicious users can inspect the source code and extract your sensitive business secrets or processes.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#secret-code](https://guide.meteor.com/security.html#secret-code)

<i data-feather="link"></i> [http://www.east5th.co/blog/2015/04/15/black-box-meteor-method-auditing/](http://www.east5th.co/blog/2015/04/15/black-box-meteor-method-auditing/)

<i data-feather="link"></i> [http://www.east5th.co/blog/2016/02/15/method-auditing-revisited/](http://www.east5th.co/blog/2016/02/15/method-auditing-revisited/)

<p class="todo-item"><i data-feather="check-square"></i> Never keep API tokens or other secrets directly in your source code.</p>

Secrets kept in code can mistakenly find their way to the client where they can be discovered and abused by malicious users.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#api-keys](https://guide.meteor.com/security.html#api-keys)

<i data-feather="link"></i> [http://www.east5th.co/blog/2015/04/15/black-box-meteor-method-auditing/](http://www.east5th.co/blog/2015/04/15/black-box-meteor-method-auditing/)

<p class="todo-item"><i data-feather="check-square"></i> Don’t expose secrets through the <code class="highlighter-rogue">public</code> field of <code class="highlighter-rogue">Meteor.settings</code>.</p>

Secrets stored in `public` will be exposed to the client.

<i data-feather="link"></i> [https://guide.meteor.com/security.html#client-settings](https://guide.meteor.com/security.html#client-settings)
