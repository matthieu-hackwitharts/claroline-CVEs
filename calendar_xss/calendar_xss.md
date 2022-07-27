# 'Location' stored XSS (version : 13.5.7)

Claroline Connect suffers from a stored xss vulnerability in 'Calendar' functionality. By adding a specific payload in the ```Location``` of an event, an attacker can
trigger an xss.

User input is reflected as an href attribute in the ```Location``` parameter. Therefore it is possible to enter a payload like ```javascript:alert(document.domain)```
to execute some javascript code.

