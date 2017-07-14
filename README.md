# Simple SMTP Proxy
- Blocks e-mails from certain countries;
- Accepts e-mails for a number of domains, and forwards to one main domain;
- Checks e-mails via ClamAV;
- Checks e-mails via SpamAssassin;
- Checks DKIM validity
- Passthrough e-mails which will not be munged into the masquerade domain, useful to proxies sending to the outside world

# TODO 
- Verify SPF (needs a means within Net::Server::Mail::SMTP to get both the sender and the connecting IP address in the same
  callback);
- Support TCP connections to ClamAV;
- Forward spams and viruses to catch-all address;
- Only allow connections from a list of IP addresses.

# AUTHOR
Nigel Horne, `<njh at bandsman.co.uk>`

# LICENSE AND COPYRIGHT
Copyright (C) 2017, Nigel Horne

Usage is subject to licence terms. The licence terms of this software are as follows:

- Personal single user, single computer use: GPL2;
- All other users (including Commercial, Charity, Educational, Government)
  must apply in writing for a licence for use from Nigel Horne at the above e-mail.
