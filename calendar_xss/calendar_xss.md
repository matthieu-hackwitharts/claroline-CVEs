# 'Location' stored XSS (CVE-2022-37162)

Claroline Connect suffers from a stored xss vulnerability in 'Calendar' functionality. By adding a specific payload in the ```Location``` of an event, an attacker can
trigger an xss.

User input is reflected as an href attribute in the ```Location``` parameter. Therefore it is possible to enter a payload like ```javascript:alert(document.domain)```
to execute some javascript code.

<br>

![xss_poc](https://raw.githubusercontent.com/matthieu-hackwitharts/claroline-CVEs/main/calendar_xss/stored_xss_calendar_new.PNG)

**Fix suggestion :** apply XSS filters on user input, and check if the entered content is a real URL.
