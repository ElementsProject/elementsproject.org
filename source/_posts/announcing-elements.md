---
title: Announcing the New Elements Project
subtitle: Open source code and developer sidechains for advancing Bitcoin.
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/_posts/announcing-elements.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/_posts/announcing-elements.md
author: martindale
---

We're excited to announce the release of [the New Elements Project][elements].
The Elements Project is a community effort to create and test new extensions to
the Bitcoin protocol.  Core Developers have already announced several of these
new Elements, including [Confidential Transactions][confidential-transactions]
by Gregory Maxwell and [Segregated Witness][segregated-witness] by Pieter
Wuille.

Along with this new release comes three new community initiatives: **A New
Sidechain Developer Community**, **A New Developer Sidechain, "Bedrock"**, and
**The Bitcoin Incubator Project**.

### New Sidechain: Bedrock
Bedrock is a new sidechain that implements _______ and ______, two Elements that
were not previously available on Alpha, our previous developer sidechain.  Alpha
will continue to operate and be maintained, but we encourage all developers to
begin using and testing with the Bedrock sidechain.  Many consensus-critical
changes are included in the new sidechain, and future work will be based on the
`betanet` branch on GitHub.

### Sidechain Developer Community
We've created [a new public Slack chat][slack] dedicated to connecting
developers working on Elements-related projects.  Slack is a convenient medium
for communication with a broader community, and does not supplant the in-depth
technical discussion that takes place in the #sidechains-dev channel on IRC.  In
fact, we've even opened up IRC access (SSL only) to the Sidechains Developer
Slack, for which you can find connection details on [the Sidechains Gateway
configuration page][sidechains-gateways].

### The Bitcoin Incubator Project
With the support of Bitcoin Core Lead Developer Wladimir van der Laan, we are
pleased to announce that a new initiative for testing changes to Bitcoin Core
has begun.  Elements that "graduate" from testnet status will enter a new
incubation period on testnet before their deployment on the main Bitcoin
network.  We hope this forms a clear path for repeatable, tested iterations and
improvements on the Bitcoin Protocol that will benefit users of all interests.

### What are Elements?
Elements are bundles of code that extend Bitcoin functionality, and today's
release includes new developer documentation on how the existing Elements work,
in addition to [a new community-managed index of available
Elements][element-list].  Everything on the Elements Project website is stored
in [the ElementsProject.org GitHub repository][github] and can be edited and
contributed to by the community. We hope that you will join us.

[elements]: https://www.elementsproject.org/
[slack]: https://chat.elementsproject.org/
[confidential-transactions]: https://www.elementsproject.org/elements/confidential-transactions
[segregated-witness]: https://www.elementsproject.org/elements/segregated-witness
[sidechains-gateways]: https://sidechains.slack.com/account/gateways
[element-list]: https://www.elementsproject.org/elements/
[github]: https://github.com/ElementsProject/elementsproject.org
