---
title: "Monitoring and taking action on a System alert"
date: 2022-08-14T21:30:20+00:00
draft: false
---

**Intended for:** Junior System Administrators

**Problem**:

Grafana is used as the monitoring tool to monitor your systems online. You have been alerted through Slack or PagerDuty that the web application is down. 

**Solution**:

The steps to troubleshoot are as follows:

- **Telnet** to the port - If you are able to telnet to the port and the service listening on the port is running and you can connect to it, then it's not a networking problem. It is good to check for the IP address to which the domain is resolved and use the same domain to test the connection.

```
`telnet  `
```

- Check if the site is accessible from another location. This will help you determine if the site is down everywhere, or if it is a problem only with your network. It is also advisable to check what the web browser returns.- Check `**whois**` to see what DNS (domain name system) servers serve the hostname to the site.

```
`whois www.test.com`
```

- Use tools like `**dig**` or `**host**` to test DNS to check if the host name can be resolved.

```
`host www.test.org `
```

-  Check global public dns servers

```
`host www.test.com 9.9.9.9`
```

If the domain is not resolved, then it is probably something to do with the DNS servers.

**If the domain issues are resolved**, troubleshoot with the below steps.

- Investigate the log files. It will give you insights into what went wrong, which service is broken. - Check the HTTP status codes. Check if any of the requests gives the response with a 5xx code. The server may be overloaded because a particular client is making a lot of connection requests to the application or a specific URL if throttling is not implemented.- Check the environment for the configurations. Maybe a configuration from the staging environment did not actually get pushed to the production.- SSL Certificate expiry.- Run out of CPU memory.