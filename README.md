# Simple SMTP Proxy

This program was put in place to work around ISPs who block outgoing port 25 for all their customers,
even those not running COTS systems.
I use this in conjunction with a cloud based machine that runs
https://github.com/vakuum/tcptunnel listening to port 2525 for connections only from my home network and then forwards
all TCP traffic to Sendmail listening locally on port 25.
That Sendmail can then send out all e-mails.

    MUA (on each machine on my LAN) -25-> smtp_proxy (on a machine labelled as a smart_host) -2525-> tcptunnel (on an Internet host) -25-> sendmail (on the same host) -25-> recipient SMTP machines

With this you can now set-up your home machine as a secondary MX.

- Blocks e-mails from certain countries;
- Accepts e-mails for a number of domains, and forwards to one main domain;
- Checks e-mails via ClamAV;
- Checks e-mails via SpamAssassin;
- Checks DKIM validity;
- Passthrough e-mails which will not be munged into the masquerade domain, useful to proxies sending to the outside world

# Installation

To install, simply put this script into /usr/local/sbin/smtp-proxy,
copy smtp-proxy.config into /usr/local/etc/smtp-proxy.config and
amend the config file to taste.

  apt install libnet-smtp-server-perl

If you are using systemd, copy and paste this content into
/etc/systemd/system/smtp-proxy.service

    [Unit]
    Description=Forward SMTP traffic
    After=network.target
    
    [Service]
    ExecStart=/usr/local/sbin/smtp-proxy
    KillMode=process
    Restart=on-failure
    
    [Install]
    WantedBy=multi-user.target

Then run

    systemctl daemon-reload
    systemctl enable smtp-proxy.service
    systemctl start smtp-proxy.service

# TODO
- Verify SPF (needs a means within Net::Server::Mail::SMTP to get both the sender and the connecting IP address in the same
  callback);
- Support TCP connections to ClamAV;
- Forward spams and viruses to catch-all address;
- Only allow connections from a list of IP addresses.

# AUTHOR
Nigel Horne, `<njh at bandsman.co.uk>`

# LICENSE AND COPYRIGHT
Copyright (C) 2017-2020, Nigel Horne

Usage is subject to licence terms. The licence terms of this software are as follows:

- Personal single user, single computer use: GPL2;
- All other users (including Commercial, Charity, Educational, Government)
  must apply in writing for a licence for use from Nigel Horne at the above e-mail.
