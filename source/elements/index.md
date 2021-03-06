---
title: "The Periodic Table of Elements"
source: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/elements/index.md
edit: https://github.com/ElementsProject/elementsproject.github.io/edit/master/source/elements/index.md
---

<style type="text/css">
  img {
    max-width: 100%;
  }

  .ui.statistic > .value {
    text-transform: none;
  }
</style>

Elements is an open source collaborative project where we work on a collection of experiments to more rapidly bring technical innovation to Bitcoin.  Elements are features that are proposed and developed in this technical community that in arbitrary combinations can be fashioned into sidechains.

## Current Elements
These are the features currently available in [Elements Core][github], the
open-source reference implementation for sidechains.  For projects built with
the latest version of Elements, such as [Liquid][liquid], you can expect them to
support each of these features.

For a list of proposed Elements, see the bottom of this document.

<div class="ui three doubling cards">
  <a class="card tooltipped" title="Blockchains keep track of the movement of tokens, and this Element allows you to create your own tokens on a sidechain." href="/elements/asset-issuance">
    <div class="image">
      <img src="/img/asset-issuance.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Ai</div>
        <div class="label">Asset Issuance</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Confidential Transactions are a new type of transaction that allow the amount of tokens being transferred to be concealed, but mathematically proven." href="/elements/confidential-transactions">
    <div class="image">
      <img src="/img/confidential-transactions.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Ct</div>
        <div class="label">Confidential Transactions</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Segregated Witness creates a separate data structure for the signature on a single transaction, fixing transaction malleability and decreasing the amount space required for storage." href="/elements/segregated-witness">
    <div class="image">
      <img src="/img/segregated-witness.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Sw</div>
        <div class="label">Segregated Witness</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
        <i class="icon setting tooltipped" title="This feature is being integrated into the Bitcoin blockchain."></i>
        <!-- <i class="icon bitcoin tooltipped" title="This feature is deployed on the Bitcoin blockchain."></i> -->
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Relative Lock Time allows a transaction to be time-locked, preventing its use in a new transaction until a relative time (generally, block height) is reached." href="/elements/relative-lock-time">
    <div class="image">
      <img src="/img/time-lock.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Rtl</div>
        <div class="label">Relative Time Lock</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Schnorr Signatures are a new way of constructing signatures for transactions, both improving performance of validating a transaction and offering new modes of multi-signature." href="/elements/schnorr-signatures">
    <div class="image">
      <img src="/img/schnorr-signatures.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Ss</div>
        <div class="label">Schnorr Signatures</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Many new opcodes are being tested, and are being hailed as 'Script 2.0'." href="/elements/opcodes">
    <div class="image">
      <img src="/img/new-opcodes.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Op</div>
        <div class="label">New Opcodes</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
        <i class="icon setting tooltipped" title="This feature is being integrated into the Bitcoin blockchain."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="This allows the signature on a transaction to be invalidated if the inputs have been spent, making it faster and easier to validate a transaction, simply by checking its signature." href="/elements/signature-covers-value">
    <div class="image">
      <img src="/img/signature-covers-value.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Scv</div>
        <div class="label">Signature Covers Value</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Deterministic Pegs allow cross-chain transactions to be constructed in a decentralized fashion.  Tokens can be moved from one blockchain to another." href="/elements/deterministic-pegs">
    <div class="image">
      <img src="/img/deterministic-pegs.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Dp</div>
        <div class="label">Deterministic Pegs</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
  <a class="card tooltipped" title="Blocks can be cryptographically signed, allowing the creator of the block to verify their identity in the future." href="/elements/signed-blocks">
    <div class="image">
      <img src="/img/signed-blocks.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Sb</div>
        <div class="label">Signed Blocks</div>
      </div>
    </div>
    <div class="extra content">
      <small>
        <i class="icon lab tooltipped" title="The Element is enabled by default."></i>
      </small>
    </div>
  </a>
</div>

## Proposed Elements
These are some of the features currently under development, but are not yet ready for deployment on a public sidechain.

<div class="ui four doubling cards">
  <a class="card tooltipped" title="Allow arbitrary, miner-rewritable bitmasks of transaction inputs and outputs." href="/elements/bitmask-sighash-modes">
    <div class="image">
      <img src="/img/bitmask-sighash-modes.svg" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">Bsm</div>
        <div class="label">Bitmask Sighash Modes</div>
      </div>
    </div>
  </a>
  <a class="card tooltipped" title="Have an Element you'd like to contribute?  Let's add it now!" href="/elements/new">
    <div class="image">
      <img src="/img/square-image.png" />
    </div>
    <div class="content">
      <div class="ui small statistic">
        <div class="value">???</div>
        <div class="label">Add a new Element <i class="icon right chevron"></i></div>
      </div>
    </div>
  </a>
</div>

[github]: https://github.com/ElementsProject/elements
[liquid]: /sidechains/liquid
