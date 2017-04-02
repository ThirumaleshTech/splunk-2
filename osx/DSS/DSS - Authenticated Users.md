# This search pulls the user that authenticated to the DSS Runtime from each log in the DSS logs directory.
# Based on a (files and directories) data input configured as follows: /YOURDEPLOYSTUDIOREPO/Logs/*.log
#
# credit to Noel Balonso - http://nbalonso.com/the-logs-talk/
#
# This data input as configured will not monitor the /Logs/Backup directory created by DSS during the imaging of multiple machines
# If the sourcetype of your data input is configured automatically or has any other name than "DSS Imaging Log" (as below), you must change that name in order for the search to work.

# You may add "| eval USERNAME=ltrim(USERNAME, "AD-DOMAIN\^") |" before the <top> portion  of this search in order to remove the AD domain prefix if some of your users have logged
# into your deploystudio server and have used a domain prefix, while others have not. Change AD-DOMAIN to the name of your AD domain.

index="yourindexhere" sourcetype="yoursourcetypehere" "was successfully authenticated." NOT "localadmin"  | rex "(?i)The user '(?P<USERNAME>[^']+)" | eval USERNAME=lower(USERNAME) | eval USERNAME=ltrim(USERNAME, "domainprefixhere\^") | top 50 USERNAME