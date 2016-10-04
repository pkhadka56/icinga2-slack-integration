# icinga2-slack-integration

###Your setup may vary, so some of the config files included here may need to be tweaked

1. Set up a new incoming webhook for your team in slack
2. Add slack-service-notification.sh to /etc/icinga2/scripts directory
3. Add the contents of slack-service-notification.conf to your templates.conf
4. Add the contents of slack-service-notification-command.conf to your commands.conf 
5. Add an entry to your notifications.conf
```
apply Notification "slack" to Service {
  import "slack-service-notification"
  user_groups = [ "oncall" ]
  interval = 30m
  assign where host.vars.notification.mail
}
```
6. Set up a new user and usergroup
```
object User "oncall_alerts" {
  import "generic-user"

  display_name = "oncall alerts"
  groups = [ "oncall" ]
  states = [ OK, Warning, Critical ]
  types = [ Problem, Recovery ]

  email = "my@email.com"
}

object UserGroup "oncall" {
  display_name = "oncall"
}
```
7. DO NOT FORGOT TO ADD YOUR OWN SLACK CHANNEL AND HOOKS IN slack-service-notification.sh
8. CHEERS!!

originally from:

https://github.com/jjethwa/icinga2-slack-notification

https://git.gmu.edu/nander13/icinga2-slack
