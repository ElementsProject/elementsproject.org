---
title: Sidechains
description: Combine multiple Elements into your own sidechain.
source: https://github.com/ElementsProject/elementsproject.github.io/blob/master/source/sidechains/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/sidechains/index.md
---

<div class="ui text container">
  <p>Sidechains are independently deployed bundles of Elements in the real world.  Sidechains can be used to test new features for Bitcoin, change network and security properties, and even stand alone as production networks.</p>

  <h4>Creating Your Own Sidechain?</h4>
  <p>Want to pick your own set of Elements, and deploy your own blockchain?</p>

  <div class="ui fluid large buttons">
    <a href="https://blockstream.com/sidechains.pdf" class="ui button">
      <i class="icon file pdf outline"></i>
      Read the Sidechains Whitepaper
    </a>
    <div class="or"></div>
    <a href="/sidechains/creating-your-own.html" class="ui positive button">
      <i class="icon leaf"></i>
      Launch Your Own Sidechain
      <i class="icon right chevron"></i>
    </a>
  </div>
</div>

# Featured
Sidechains with a working network can be listed here.  <a href="https://github.com/ElementsProject/elementsproject.org/edit/master/source/sidechains/index.md">Add Yours &raquo;</a>

## Experimental Sidechains
These sidechains are in development and testing, or are explicitly intended for non-production use.

<div class="ui two stackable cards">
  <div class="card" style="background: url('/img/platonic-solids.png');">
    <div class="ui image centered tiny" style="background: none;" />
      <img src="/img/0-14-1.png" style="margin: 3em 0; width: 100%;" />
    </div>
    <div class="content" style="background: white;">
      <h3 class="header">[Elements 0.14.1](/sidechains/creating-your-own.html)</h3>
      <p class="description">Elements 0.14.1 is the latest version and includes most of [the stable Elements][stable-elements]. It is a convenient way of prototyping your application before going to production.</p>
    </div>
    <div class="extra content">
      <a href="/sidechains/creating-your-own.html" class="ui primary fluid button">Create Your Own Sidechain</a>
    </div>
  </div>
  <div class="card" style="background: url('/img/platonic-volumes.png') 100%;">
    <div class="ui image centered tiny" style="background: none;" />
      <img src="/img/alpha.png" style="margin: 3em 0; width: 100%;" />
    </div>
    <div class="content" style="background: white;">
      <h3 class="header">[Alpha](/sidechains/alpha)</h3>
      <p class="description">Alpha is an older version of Elements. This documentation is outdated, and will eventually be removed. Elements Alpha does not support recent elements features, or receive backported security fixes.</p>
    </div>
    <div class="extra content">
      <a href="/sidechains/alpha" class="ui primary fluid button">Learn More about Alpha</a>
    </div>
  </div>
  <div class="card" style="background: url('/img/forest.jpg');">
    <div class="ui image centered tiny" style="background: none;" />
      <img src="/img/rootstock-white.webp" style="margin: 3em 0; width: 100%;" />
    </div>
    <div class="content" style="background: white;">
      <h3 class="header">[Rootstock](/sidechains/rootstock)</h3>
      <p class="description">Rootstock is a sidechain that implements robust smart contracts.  Rootstock is backwards-compatible with Ethereum, so scripts from the Ethereum ecosystem can run directly on a Bitcoin-backed sidechain.</p>
    </div>
    <div class="extra content">
      <a href="/sidechains/rootstock" class="ui primary fluid button">Learn More about Rootstock</a>
    </div>
  </div>
  <div class="card" style="background: linear-gradient(to right, #008bbe 0%, #13e1d0 100%);">
    <div class="ui image centered tiny" style="background: none;" />
      <img src="/img/gem.png" style="margin: 3em 0; width: 100%;" />
    </div>
    <div class="content" style="background: white;">
      <h3 class="header">[Gem](/sidechains/gem)</h3>
      <p class="description">Gem Health is a network for developing applications and shared infrastructure for healthcare. We are building the fabric of a globally integrated healthcare continuum that’s designed to make healthcare more personal and affordable.</p>
    </div>
    <div class="extra content">
      <a href="/sidechains/gem" class="ui primary fluid button">Learn More about Gem</a>
    </div>
  </div>
</div>

## Production Sidechains
These sidechains are being used on the main Bitcoin network.

<div class="ui cards">
  <div class="ui fluid card">
    <div class="ui image centered medium" style="background: none;" />
      <img src="/img/liquid-logo.png" style="margin: 3em 0; width: 100%;" />
    </div>
    <div class="content">
      <h3 class="header">[Liquid](/sidechains/liquid)</h3>
      <p class="description">Liquid is the first commercial sidechain by Blockstream.  It enables instant movement of funds between exchanges, without waiting for the delay of confirmation in the Bitcoin blockchain.  It is available to users of participating Bitcoin exchanges.</p>
    </div>
    <div class="extra content">
      <a href="/sidechains/liquid" class="ui primary fluid button">Learn More About Liquid</a>
    </div>
  </div>
</div>


[stable-elements]: https://elementsproject.org/elements#stable
