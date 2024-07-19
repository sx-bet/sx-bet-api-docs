---
toc_footers:
  - <a href='https://sx.bet'>Visit sx.bet</a>

title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

includes:
  - rollupmigrationguide
  - testnet
  - metadata
  - websocket
  - apiKey
  - leagues
  - sports
  - fixtures
  - livescores
  - markets
  - parlaymarkets
  - trades
  - orders
  - unitconversion
  - eip712signing
  - fees

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the SX.bet API
---

# Introduction

Be your own bookmaker or fill orders programmatically with the SX.bet API!

Technical questions or need support? [Send us an e-mail](mailto:api-support@sx.bet). 

We support betting in USDC, WETH, and WSX

DEPRECATED: If you wish to use our wrapper for javascript you can do so [here](https://github.com/sportx-bet/sportx-js)

| Token | SX Network Address                           |
| ----- | -------------------------------------------- |
| USDC  | `0xe2aa35C2039Bd0Ff196A6Ef99523CC0D3972ae3e` |
| WETH  | `0xA173954Cc4b1810C0dBdb007522ADbC182DaB380` |
| WSX   | `0xaa99bE3356a11eE92c3f099BD7a038399633566f` |

Explorer available [here](https://explorer.sx.technology) 

<aside class="notice">
All ETH addresses used in this API are in check-summed format. If you pass in lowercase-only addresses, you won't get results.
</aside>
