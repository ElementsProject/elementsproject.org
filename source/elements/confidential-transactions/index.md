#### Confidential Transactions 
*Principal Investigator: Greg Maxwell* [[_Peer reviewed technical details_](https://github.com/ElementsProject/elementsproject.github.io/blob/master/confidential_values.md)]

One of the most powerful new features being explored in Elements is Confidential Transactions. This keeps the amounts transferred visible only to participants in the transaction (and those they designate), while still guaranteeing that no more coins can be spent than are available in a cryptographic way.

This goes a step beyond the usual privacy offered by Bitcoin’s blockchain, which relies purely on pseudonymous - but public - identities. This matters, because insufficient financial privacy can have serious security and privacy implications for both commercial and personal transactions. Without adequate protection, thieves and scammers can focus their efforts on known high-value targets, competitors can learn business details, and negotiating positions can be undermined. 

The most visible implication of Confidential Transactions is the introduction of a new address type (confidential addresses). These are longer than usual as they also includes a blinding key for the values. They are the default address type in Alpha.
