# ansible-role-tor

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-tor.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-tor)

RHEL/CentOS - Anonymizing overlay network for TCP

## Requirements

None

## Role Variables

All default variables are listed below

    torrc:
      CookieAuthentication: 1
      CookieAuthFile: /run/tor/control.authcookie
      CookieAuthFileGroupReadable: 1
      ControlSocket: /run/tor/control
      ControlSocketsGroupWritable: 1
    torrc_hiddenservices: []
    torsocks:
      OnionAddrRange: 127.42.42.0/24
      TorAddress: 127.0.0.1
      TorPort: 9050

## Dependencies

 * https://galaxy.ansible.com/linuxhq/epel/
 
## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.tor
          torrc:
            AccountingMax: '30 GB'
            AccountingStart: 'day 00:00'
            CookieAuthentication: 1
            CookieAuthFile: /run/tor/control.authcookie
            CookieAuthFileGroupReadable: 1
            ContactInfo: 'Tor Project <tor@linuxhq.org>'
            ControlSocket: /run/tor/control
            ControlSocketsGroupWritable: 1
            ExitPolicy:
              - 'reject *:*'
            ORPort: 9001
            Nickname: "{{ inventory_hostname.split('.')[3] }}"
            RelayBandwidthBurst: '1024 KBytes'
            RelayBandwidthRate: '512 KBytes'
    
## License

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
