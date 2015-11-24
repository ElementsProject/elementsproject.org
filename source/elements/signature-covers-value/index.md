#### Signature Covers Value
*Principal Investigator: Glenn Willen*

The signatures verified by the CHECKSIG operators now cover the output value of spent inputs. This avoids the need for hardware signing devices to know the full previous transactions whose outputs are spent; if they are being lied to, the resulting signature is invalid anyway.

A side effect of this change is that signing now needs to know the values (blinded or not) consumed by the transaction’s inputs.
