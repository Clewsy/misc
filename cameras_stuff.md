# 1 - hallway

## Admin:
- url: http://hallway/
- ugh, needs IE

## Stream:
- url: http://hallway.lan/mjpeg.cgi
- log in as admin

# 2 - lounge

## Admin
- url: http://donbot
- log in as root

## Stream:
- url: rtsp://donbot.lan:8888/unicast
- user: b4t
- resolution: 1280x720

# 3 - b4t-cam

## Admin:
- Standard motion on raspbian deployed with ansible.

## Stream:
- http://b4t-cam:8888
- resolution: 640x480

# 4 - pazuzu

## Admin:
- Standard motion on raspbian deployed with ansible.

## Stream:
- http://pazuzu:8888
- resolution: 640x480


# Action commands:
```yaml
action_buttons:
  - type: up
    camera: 1
    command: 'curl -u admin:password http://hallway.lan/config/ptz_move_rel.cgi -d"t=5"'
  - type: down
    camera: 1
    command: 'curl -u admin:password http://hallway.lan/config/ptz_move_rel.cgi -d"t=-5"'
  - type: left
    camera: 1
    command: 'curl -u admin:password http://hallway.lan/config/ptz_move_rel.cgi -d"p=-5"'
  - type: right
    camera: 1
    command: 'curl -u admin:password http://hallway.lan/config/ptz_move_rel.cgi -d"p=5"'
  - type: preset1
    camera: 1
    command: 'curl -u admin:password http://hallway.lan/config/ptz_move.cgi -d"p=180" -d"t=50"'
  - type: preset2
    camera: 1
    command: 'curl -u admin:password http://hallway.lan/config/ptz_move.cgi -d"p=0" -d"t=0"'

  - type: up
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=motor_up" -d"val=50" > /dev/null'
  - type: down
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=motor_down" -d"val=50" > /dev/null'
  - type: left
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=motor_left" -d"val=50" > /dev/null'
  - type: right
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=motor_right" -d"val=50" > /dev/null'
  - type: preset1
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=motor_calibrate" > /dev/null'
  - type: light_on
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=ir_cut_off" > /dev/null && curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=ir_led_on" > /dev/null'
  - type: light_off
    camera: 2
    command: 'curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=ir_cut_on" > /dev/null && curl --insecure --silent --user root:password https://donbot.lan/cgi-bin/action.cgi -d"cmd=ir_led_off" > /dev/null'

  - type: light_on
    camera: 3
    command: 'curl -s http://p0wer.lan/index.php?a=on >> /dev/null'
  - type: light_off
    camera: 3
    command: 'curl -s http://p0wer.lan/index.php?a=off >> /dev/null'
```




