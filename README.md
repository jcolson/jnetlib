# Java Network Library
built to encompass such things as Cisco's TACACS protocol -- by @Jay_Colson

## Cisco TACACS protocol information


```
/**
 * @author Jay_Colson, Copyright 2000
 * @version v0.10, 06/13/2000
 */
packet construction:

HEADER
4 bits - major version (0xc)
4 bits - minor version (0x0 default, 0x1 minor_ver_one)
8 bits - type (0x01 authentication, 0x02 authorization, 0x03 accounting)
8 bits - seq_no (first packet must be 1, clients only send odd, server sends even)
8 bits - flags (0x01 is unencrypted flag, 0x04 is single connect flag)
32 bits - session_id (id for session, does not change for duration, random generated)
32 bits - length (length of packet BODY, not including the HEADER)

BODY
Authentication START packet
	8 bits - action (0x01 Login, 0x02 Chpass, 0x04 Sendauth)
	8 bits - priv_lvl (0x0f Max, 0x00 Min)
	8 bits - authen_type (0x01 ascii, 0x02 pap, 0x03 chap, 0x04 arap, 0x05 mschap)
	8 bits - service (0x00 nonw, 0x01 login, 0x02 enable, 0x03 ppp, ....)
	8 bits - user_len 
	8 bits - port_len
	8 bits - rem-addr_len
	8 bits - data_len
	? bits - user (username optional in START packet)
	? bits - port (ascii name of client port - tty01)
	? bits - rem_addr (ascii string desc client remote location)
	? bits - data (used to send data for action and authen_type)
	
Authentication REPLY packet
	8 bits - status (0x01 pass, 0x02 fail, 0x03 getdata, 0x04 getuser, 0x05 getpass, 0x06 restart, 0x07 error, 0x21 follow)
	8 bits - flags (0x01 noecho)
	16 bits - server_msg_len
	16 bits - data_len
	? bits - server_msg (message to be displayed to user, optional)
	? bits - data (data intended for NAS, not user)
	
Authentication CONTINUE packet
	16 bits - user_msg_len
	16 bits - data_len
	8 bits - flags (0x01 abort)
	? bits - user_msg (data user/NAS responds with to server_msg from REPLY)
	? bits - data (used to send data for action and authen_type)
```
	
