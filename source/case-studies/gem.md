---
title: Gem's Use of Elements & Sidechains
description: Learn about how Gem is using Elements in their sidechain implementation.
source: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/case-studies/gem.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/case-studies/gem.md
---


<div class="ui comments">
  <div class="comment">
    <div class="content">
      <strong class="author">Matt Smith</strong>
      <div class="metadata">Lead Developer, Gem</div>
      <div class="text">
        <p>Our interest is mostly in the asset issuance implementation I've been discussing with Jorge. We're currently prototyping blockchain-based systems that track ownership of arbitrary asset classes. While we're also working with other technologies that apply asset issuance as a protocol on top of a blockchain network like OpenAssets, there are features required for some applications that we can only get out of native, consensus-enforced asset management.</p>

        <p>Additionally, we use Confidential Transactions for (among other things) implementing a subset of the access controls in those systems, and having a working implementation of CT (which is compatible with asset management) is an huge boon.</p>

        <p>Finally, we're exploring use of the two-way peg itself, demonstrated by Alpha, to build interoperability into these systems from the beginning. Cross-organizational compatibility of asset tracking systems comes for free as long as those systems are build on a chain with a sufficiently expressive scripting language and that's a big win.</p>
      </div>
    </div>
  </div>
</div>
