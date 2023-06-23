# Parlay Markets

Bettors can request a custom parlay on [SX.Bet](https://sx.bet) by selecting multiple markets. When they submit a parlay request, a message is sent via Websocket (See [this link](#parlay-market-requests) for more details on the request). Once this message is sent, the web client will wait three seconds to allow market makers to submit orders for the parlay market.

Market makers can use the payload data from the Parlay Request to submit an [order](#post-a-new-order). Market makers have a three second window to post orders. After this point, bettors will be shown all available orders at the same time and no other orders will be added.

Bettors can choose which order to take and will be able to fill orders like any other non-parlay order.

Market makers can [cancel](#cancel-individual-orders) orders like any other non-parlay order.

<aside class="notice">
Parlay order book that displays to bettor will automatically close after one minute. Your orders may still be active even though the order book window has closed (the user will not be able to view your order after the window closes).
</aside>

<aside class="notice">
Parlay Orders will expire just as normal orders do, so please set the `apiExpiry` on your orders accordingly.
</aside>

<aside class="notice">
Parlay Markets act as regular markets, but with additional fields to indicate the underlying legs that make up the Parlay.
</aside>