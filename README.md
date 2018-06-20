# ansible-role-tor

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-tor.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-tor)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-tor-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/tor)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

Linux - Anonymizing overlay network for TCP

## Requirements

This role requires that you have the epel repository installed, if RedHat.

 * https://galaxy.ansible.com/linuxhq/epel/

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
      AllowInbound: 0
      AllowOutboundLocalhost: 0
      IsolatePID: 0
      OnionAddrRange: 127.42.42.0/24
      TorAddress: 127.0.0.1
      TorPort: 9050

## Dependencies

None
 
## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.tor
          torrc:
            AccountingMax: '30 GB'
            AccountingStart: 'day 00:00'
            CellStatistics: 1
            CookieAuthentication: 1
            CookieAuthFile: /run/tor/control.authcookie
            CookieAuthFileGroupReadable: 1
            ConnDirectionStatistics: 1
            ConnLimit: 1000
            ContactInfo: 'Tor Project <tor@linuxhq.org>'
            ControlSocket: /run/tor/control
            ControlSocketsGroupWritable: 1
            DirReqStatistics: 1
            EntryStatistics: 1
            ExitPolicy:
              - 'reject *:*'
            ExitRelay: 0
            ExtraInfoStatistics: 1
            HiddenServiceStatistics: 1
            Nickname: "{{ inventory_hostname.split('.')[3] }}"
            ORPort: 9001
            RelayBandwidthBurst: '1024 KBytes'
            RelayBandwidthRate: '512 KBytes'
            Sandbox: 1
          torrc_hiddenservices:
            - dir: external
              ports:
                80: '127.0.0.1:80'
              private_key: |
                -----BEGIN RSA PRIVATE KEY-----
                {...}
                -----END RSA PRIVATE KEY-----
          torsocks:
            AllowInbound: 0
            AllowOutboundLocalhost: 0
            IsolatePID: 1
            OnionAddrRange: 127.42.42.0/24
            TorAddress: 127.0.0.1
            TorPort: 9050

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
