# Defensive Coding

## 1. Trust

- The most crucial principle of security
- Do we trust the integrity of request coming in from the user's browser?
- Do we trust that upstream services have done the work to make our data clean and safe?
- do we trust the connection between the user's browser and our application cannot be tampered?
- Do we trust that the services and data stores we depend on?
- We need to efficiently manage our risk

## 2. Reject Unexpected Form Input

- White list when you can
- Black list when you can't whitelist
- Keep contract restrictive
- Alert about the possible attack
- Avoid reflecting input back to a user
- Reject web content before it gets deeper into application logic

## 3. Encode HTML Output

- Output encode all application data
- Use framework's encoding capability
- Avoid nested rendering contexts
- Store your data in raw form and encode at rendering time
- Avoid unsafe framework and Javascript calls that avoid encoding

## 4. Bind Parameters for Databases

- Avoid building SQL from user input
- Bind all parameterized data,
- Use the native driver binding function rather than trying to handle the encoding yourself
- Don't think stored procedures or ORM tools will save you. You need to use binding functions for those, too
- NoSQL doesn't make you injection-proof

## 5. Protect Data in Transit

- Use HTTPS for everything
- Use HSTS to enforce it
  - requests that a browser ONLY interacts with the website over HTTPS
  - redirecting from HTTP to HTTPS is not the same because it presents the same risks as any request sent over ordinary HTTP
- Certificate from trusted certificate authority
- Protect your private key
- Use a configuration tool to help adopt a secure HTTPS configuration
- Set the "secure" flag in cookies
- Be mindful not to leak sensitive data in URLs
- Verify your server configuration after enabling HTTPS and every few months thereafter
