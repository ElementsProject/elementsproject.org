---
title: Announcing the New Elements Project
subtitle: Open source code and developer sidechains for advancing Bitcoin.
source: https://github.com/ElementsProject/elementsproject.github.io/blob/hexo/source/_posts/announcing-elements.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/_posts/announcing-elements.md
author: martindale
---

On the heels of the [Scaling Bitcoin workshop in Hong
Kong][scaling-bitcoin-hong-kong], we're excited to announce the release of [the
New Elements Project][elements]. The Elements Project is a community effort to
create and test new extensions to the Bitcoin protocol.  Core Developers have
already announced several of these new Elements, including [Confidential
Transactions][confidential-transactions] by Gregory Maxwell and [Segregated
Witness][segregated-witness] by Pieter Wuille, which have undergone extensive
testing on existing sidechains.
<!-- more -->

Along with this new release also comes a new community initiative, **[the
Sidechain Developer Community][contributing].**  We're hoping this community
will facilitate discussion around how various Elements are being used, including
known efforts by companies like Gem and RootStock.

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/9pyVvq-vrrM" frameborder="0" allowfullscreen></iframe>
</center>

### What are Elements?
Elements are bundles of code that extend Bitcoin functionality, and today's
release includes new developer documentation on how the existing Elements work,
in addition to [a new community-managed index of available
Elements][element-list].  Everything on the Elements Project website is stored
in [the ElementsProject.org GitHub repository][github] and can be edited and
contributed to by the community. We hope that you will join us.

### A Publicly Editable Resource
We've made the entire Elements Project website a [publicly editable
resource][github], and even added simple buttons to most pages that link
directly to graphical editors for quick fixes.  We want the Elements Project to
be a community resource, including the highlighting of projects that make use of
Elements, or are otherwise deployed on a sidechain.

Contributing to the Elements Project website should be very familiar to most 
developers, but the graphical editor makes it accessible to all.  If you'd like 
to contribute, head over to [the Contributing guide][contributing].

### Sidechain Developer Community
We've created [a new public Slack chat][slack] dedicated to connecting
developers working on Elements-related projects.  Slack is a convenient medium
for communication with a broader community, and does not supplant the in-depth
technical discussion that takes place in [the #sidechains-dev channel on
IRC][irc].  In fact, we've even opened up IRC access (SSL only) to the
Sidechains Developer Slack, for which you can find connection details on [the
Sidechains Gateway configuration page][sidechains-gateways].

<div class="ui vertical stripe segment" style="padding: 0; border: 0;">
  <p>Our public Slack is the fastest way to get connected with other contributors to the Elements Project.  We'll send an invitation to your email address.</p>
  <a href="https://chat.elementsproject.org/" class="ui button primary huge" style="float:right;">Join the Community<i class="icon right chevron"></i></a>
  <div style="clear: both;"></div>
</div>

### Next Steps
Segregated Witness has been deployed on [the `alpha` sidechain for some
time][alpha], but as the first Element that is likely to make its way into
Bitcoin Core, it is important that it undergoes rigorous review.  Discussion is
ongoing in [the Developer Mailing list][sidechains-list], but you can use it today by [getting
connected to the `alpha` network][alpha-moving-coins].

Until then, [join the Sidechains chat][slack] and get acquainted with your fellow
developers!

[elements]: https://www.elementsproject.org/
[slack]: https://chat.elementsproject.org/
[confidential-transactions]: https://www.elementsproject.org/elements/confidential-transactions
[segregated-witness]: https://www.elementsproject.org/elements/segregated-witness
[sidechains-gateways]: https://sidechains.slack.com/account/gateways
[element-list]: https://www.elementsproject.org/elements/
[github]: https://github.com/ElementsProject/elementsproject.org
[contributing]: https://www.elementsproject.org/contributing/
[scaling-bitcoin-hong-kong]: https://www.scalingbitcoin.org/hongkong2015
[irc]: https://www.elementsproject.org/contributing/#irc
[alpha]: https://www.elementsproject.org/sidechains/alpha
[alpha-build]: https://www.elementsproject.org/sidechains/alpha#Build_Instructions
[alpha-moving-coins]: https://www.elementsproject.org/sidechains/alpha#Moving_coins_between_Testnet_and_Alpha
[sidechains-list]: https://lists.linuxfoundation.org/mailman/listinfo/sidechains-dev
