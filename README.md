#autogen_hosts - Regularly update etc/hosts file with Halo server names

Version: *1.0*
<br />
Author: *Tim Spencer* - *tspencer@cloudpassage.com*

These scripts regularly update the /etc/hosts file on each Halo-protected server with both the name and IP address of every other server, so that syslog entries will specify server name as well as IP address.


##Requirements and Dependencies

To run, this set of scripts requires:

* Ruby installed on the host on which the hosts.rb script runs
* Ruby gems: oauth2, rest-client, json
* A full-access Halo API key (obtained from the Halo Portal)


##List of Files

* **install.sh**  -  *Copies the hosts file, sets up the cron job, installs hosts.rb*
* **hosts.rb**  -  *main script file; it extracts server information from CloudPassage API*
* **hosts2.rb**  -  *alternate main script file; shows a different way to authenticate to the API*
* **hostsupdate.cron**  -  *cron job that updates a server's /etc/hosts file with Halo-defined server name and address*
* **README.md**  -  *This ReadMe file*
* **LICENSE.txt**  -  *License from CloudPassage*


##Usage

We have a centralized syslog host.  Since we generally don't maintain
reverse dns for our servers, we end up with the log files generated by
syslog named after IP addresses, which makes it harder for us to figure out
who is generating what.

But if you generate an /etc/hosts from the hosts in CloudPassage, you can fix
all that and make it so that most things are named properly!  This presumes
that you set your hostnames properly.  AWS doesn't do that by default, although
it is easily fixed if you are using something like RightScale to manage the servers.

1. Edit hosts.rb (or hosts2.rb) to add the two parts of your Halo API key.
1. In hostsupdate.cron, set the cron frequency that you want (default = 30 minutes).
1. Run install.sh.

hostsupdate.cron will now run at the frequency you have set, calling hosts.rb to update the set of servers, and then updating every server's hosts file with that info.

<!---
#CPTAGS:community-unsupported integration automation
#TBICON:images/ruby_icon.png
-->
