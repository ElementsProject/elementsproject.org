---
title: Elements
source: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/hexo/source/elements/index.md
---

<style type="text/css">
  img {
    max-width: 100%;
  }
</style>

Elements is an open source collaborative project where we work on a collection of experiments to more rapidly bring technical innovation to Bitcoin.  Elements are features that are proposed and developed in this technical community that in arbitrary combinations can be fashioned into sidechains.

<center>
[![Greg Maxwell's Sidechain Elements Intro Video](http://i.imgur.com/AsSENaW.png)](https://www.youtube.com/watch?v=9pyVvq-vrrM)
</center>

## Current Elements
These are the features under currently under investigation as part of the Alpha dev sidechain.

<div class="ui four doubling cards">
  <a class="card tooltipped" title="Confidential Transactions are a new type of transaction that allow the amount of tokens being transferred to be concealed, but mathematically proven." href="/elements/confidential-transactions">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Ct</div>
        <div class="label">Confidential Transactions</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Segregated Witness creates a separate data structure for the signature on a single transaction, fixing transaction malleability and decreasing the amount space required for storage." href="/elements/segregated-witness">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Sw</div>
        <div class="label">Segregated Witness</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Relative Lock Time allows a transaction to be time-locked, preventing its use in a new transaction until a relative time (generally, block height) is reached." href="/elements/relative-lock-time">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">RTL</div>
        <div class="label">Relative Time Lock</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Schnorr Signatures are a new way of constructing signatures for transactions, both improving performance of validating a transaction and offering new modes of multi-signature." href="/elements/schnorr-signatures">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">S<span style="text-transform:lowercase;">S</span></div>
        <div class="label">Schnorr Signatures</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Many new opcodes are being tested, and are being hailed as 'Script 2.0'." href="/elements/opcodes">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Op</div>
        <div class="label">New Opcodes</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="This allows the signature on a transaction to be invalidated if the inputs have been spent, making it faster and easier to validate a transaction, simply by checking its signature." href="/elements/signature-covers-value">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">SCV</div>
        <div class="label">Signature Covers Value</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Deterministic Pegs allow cross-chain transactions to be constructed in a decentralized fashion.  Tokens can be moved from one blockchain to another." href="/elements/deterministic-pegs">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">DP</div>
        <div class="label">Deterministic Pegs</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Blocks can be cryptographically signed, allowing the creator of the block to verify their identity in the future." href="/elements/signed-blocks">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">SB</div>
        <div class="label">Signed Blocks</div>
      </div>
    </div>
  </a>
</div>

## Proposed Elements
These are some of the features currently under development, but are yet ready for testing in dev sidechain.

<div class="ui four doubling cards">
  <a class="card tooltipped" title="Blockchains keep track of the movement of tokens, and this Element allows you to create your own tokens on a sidechain." href="/elements/asset-issuance">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">AI</div>
        <div class="label">Asset Issuance</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Allow arbitrary, miner-rewritable bitmasks of transaction inputs and outputs." href="/elements/bitmask-sighash-modes">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">BSm</div>
        <div class="label">Bitmask Sighash Modes</div>
      </div>
    </div>
  </a>
</div>
