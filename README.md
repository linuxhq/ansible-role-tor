# ansible-role-tor

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-tor.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-tor)

RHEL/CentOS -  Anonymizing overlay network for TCP

## Requirements

None

## Role Variables

All default variables are listed below

    tor_datadirectory: /var/lib/tor
    tor_controlsocket: /run/tor/control
    tor_controlsocketsgroupwritable: True
    tor_cookieauthentication: True
    tor_cookieauthfile: /run/tor/control.authcookie
    tor_cookieauthfilegroupreadable: True
    tor_runasdaemon: False
    torsocks_address: 127.0.0.1
    torsocks_allowinbound: False
    torsocks_allowoutboundlocalhost: False
    torsocks_isolatepid: False
    torsocks_onionaddrrange: 127.42.42.0/24
    torsocks_torport: 9050

Additional variables for tor listed below (per default torrc)

    tor_accountingmax: '40 GBytes'
    tor_accountingstart: 'day 00:00'
    tor_address: noname.example.com
    tor_bridgerelay: True
    tor_contactinfo: '0xFFFFFFFF Random Person <nobody AT example dot com>'
    tor_dirport: 9030
    tor_dirportfrontpage: /etc/tor/tor-exit-notice.html
    tor_exitpolicy:
      - 'accept *:6660-6667,reject *:*'
      - 'accept *:119'
      - 'accept *4:119'
      - 'accept6 *6:119'
      - 'reject *:*' 
    tor_publishserverdescriptor: False
    tor_relaybandwidthburst: '200 KBytes'
    tor_relaybandwidthrate: '100 KBytes'
    tor_controlport: 9051
    tor_hashedcontrolpassword: '16:872860B76453A77D60CA2BB8C1A7042072093276A3D701AD684053EC4C'
    tor_hiddenservices:
      hidden_service:
        ports:
          - src: 80
            dst: '127.0.0.1:80'
          - src: 22
            dst: '127.0.0.1:22'
    tor_log:
      - notice file /var/log/tor/notices.log
      - debug file /var/log/tor/debug.log
      - notice syslog
      - debug stderr
    tor_myfamily:
      - keyid1
      - keyid2
    tor_nickname: ididnteditheconfig
    tor_orport: 9001
    tor_outboundbindaddress: 10.0.0.5
    tor_sockspolicy:
      - 'accept 192.168.0.0/16'
      - 'accept6 FC00::/7'
      - 'reject *'
    tor_socksport: 9050

Additional variables for torsocks listed below (per default torsocks.conf)

    torsocks_password: password
    torsocks_username: login

You can also define additional tor variables by defining the following

    tor_additional_parameters:
      CountPrivateBandwidth: 1
      LearnCircuitBuildTimeout: 1
      FirewallPorts: 6667

## Dependencies

 * https://galaxy.ansible.com/linuxhq/epel/
 
## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.tor
          tor_accountingmax: '20 GB'
          tor_accountingstart: 'day 00:00'
          tor_contactinfo: 'Tor Project <tor@linuxhq.org>'
          tor_exitpolicy:
            - 'reject *:*'
          tor_orport: 9001
          tor_nickname: linuxhq
    
## License

BSD

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
