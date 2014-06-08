
===========================================================
Can regex match intersection between two regular expressions?
===========================================================



For **And** operation, we have something like this in RegEx

(REGEX+=?)(REGEX+=?)

Taking your example

```js
'Cat'.match(/([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)$/)
["Cat", "C", "a", "t"]
'Ca'.match(/([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)$/)
//null
'Cat123'.match(/([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)$/)
//null
```

**where**

`([A-Za-z]+=?)`  //Match All characters

**and**

`([aeiouAEIOU]+=?)` //Match all vowels


Combine them both will match

'([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)`

**eg:**

```js
'Hmmmmmm'.match(/([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)$/)
//null
'gthb'.match(/([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)$/)
//null
'github'.match(/([A-Za-z]+=?)([aeiouAEIOU]+=?)([A-Za-z]+=?)$/)
//["github", "gith", "u", "b"]
```