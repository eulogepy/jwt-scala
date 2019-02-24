## JwtClaim Case Class

```scala
scala> import pdi.jwt.JwtClaim
import pdi.jwt.JwtClaim

scala> JwtClaim()
res0: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@97c880b6

scala> // Specify the content as JSON string
     | // (don't use var in your code if possible, this is just to ease the sample)
     | var claim = JwtClaim("""{"user":1}""")
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@a0b74282

scala> // Append new content
     | claim = claim + """{"key1":"value1"}"""
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@85390be2

scala> claim = claim + ("key2", true)
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@102a1db1

scala> claim = claim ++ (("key3", 3), ("key4", Seq(1, 2)), ("key5", ("key5.1", "Subkey")))
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@c18a9898

scala> // Stringify as JSON
     | claim.toJson
res5: String = {"user":1,"key1":"value1","key2":true,"key3":3,"key4":[1,2],"key5":{"key5.1":"Subkey"}}

scala> // Manipulate basic attributes
     | // Set the issuer
     | claim = claim.by("Me")
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@b2b0c595

scala> // Set the audience
     | claim = claim.to("You")
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@3e1a2d74

scala> // Set the subject
     | claim = claim.about("Something")
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@b6c24fa3

scala> // Set the id
     | claim = claim.withId("42")
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@b5d231f8

scala> // Set the expiration
     | // In 10 seconds from now
     | claim = claim.expiresIn(5)
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@ea81efb

scala> // At a specific timestamp (in seconds)
     | claim.expiresAt(1431520421)
res14: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@c7898aca

scala> // Right now! (the token is directly invalid...)
     | claim.expiresNow
res16: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@e0c8d795

scala> // Set the beginning of the token (aka the "not before" attribute)
     | // 5 seconds ago
     | claim.startsIn(-5)
res19: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@4f5d6b9

scala> // At a specific timestamp (in seconds)
     | claim.startsAt(1431520421)
res21: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@8b1963e9

scala> // Right now!
     | claim = claim.startsNow
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@83a7d1be

scala> // Set the date when the token was created
     | // (you should always use claim.issuedNow, but I let you do otherwise if needed)
     | // 5 seconds ago
     | claim.issuedIn(-5)
res26: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@39052a40

scala> // At a specific timestamp (in seconds)
     | claim.issuedAt(1431520421)
res28: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@66a33710

scala> // Right now!
     | claim = claim.issuedNow
claim: pdi.jwt.JwtClaim = pdi.jwt.JwtClaim@24553a9b

scala> // We can test if the claim is valid => testing if the current time is between "not before" and "expiration"
     | claim.isValid
res31: Boolean = true

scala> // Also test the issuer and audience
     | claim.isValid("Me", "You")
res33: Boolean = true

scala> // Let's stringify the final version
     | claim.toJson
res35: String = {"iss":"Me","sub":"Something","aud":["You"],"exp":1551004391,"nbf":1551004386,"iat":1551004386,"jti":"42","user":1,"key1":"value1","key2":true,"key3":3,"key4":[1,2],"key5":{"key5.1":"Subkey"}}
```