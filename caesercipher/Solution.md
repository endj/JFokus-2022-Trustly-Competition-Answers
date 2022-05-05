In this question we are given instructions on how to encrypt a message 
using a scheme but we have to figure out the decryption method ourselves.

Consider the smaller example with the encrypted message "DEAD COFFE"

If we are given the available characters

[_,A,B,C,D,E,F]

"Character Rotations":

[3,7,1,9,5,2,3]

Encrypted Message:

"ADEAFFB C"

and a initial number of rotations we should be able to reconstruct the 
cipher in the correct position at least for the first value.

Initial cipher:

[D,E,F,_,A,B,C]


If we look at the first encrypted character "A", we know that during encryption, it was mapped to the same index in the initial 
position of the starting cipher configuration. This is clear from the encryption instructions.

After a lookup we can decrypt the first character in the message which must have been a "D" cause "A" maps to "D" in 
the initial cipher. Likewise, we know that when the next character was encrypted, the cipher was rotated by the rotation
value of the decrypted character "A". By starting from the first known position and working backwards we can figure out
all positions the cipher must have been in during encryption.

PseudoCode:

```
decrypt(encryptedMessage) {
	decryptedMessage

	for char in encryptedMessage {
		decodedChar = availableCharacters[indexOf(encryptedChar)]
		rotationValue = rotationValues[indexOf(decodedChar)]
		rotate(cipher, rotationValue)
        decryptedMessage += decodedChar
	}

	return decryptedMessage
} 
```
