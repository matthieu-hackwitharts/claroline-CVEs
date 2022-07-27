# Stored XSS via SVG file upload (version : 13.5.7)

Claroline Connect presents a stored xss vulnerability because of the possibility to upload an arbitrary svg file, which is one of the allowed image types. 
Several upload forms can be used, I've personnally choosed the resource icon upload.

By crafting a svg file which contains some javascript, an attacker can trigger some xss payload.

