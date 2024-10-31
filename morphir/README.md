# morphir-trader```


Flow Control (request purchase)

1. Request to complete an order with a New order
TradeOrder Request
       |
       v
 Validation of Action(state) --> Failed Step --> Failed Action
       |
       v
 Check if market closed ->  Return Trade(with Dfd status)
       |
       v
  BUY --> check if client has enough                             SELL -> check if client has minimum security in order
       |                                                                                       |
       v                                                                                     <--
  Full Purchase         Partial Purchase -
       |                     |
       v                     v
  Return Settled         Return Trade with status Partial Fill



2. Cancel existing order

TradeOrder Request (Cancel order)
       |
       v
Validate (Required to be New,PROCESSING) - > Failed Action
       |
       v
if New          ->  continue to cancel order    -> return order
if Processing   ->  check if partial fill       -> if side is BUY -> debit account for completed securities
                                                   if side is SELL -> credit acc for completed securities
                                                   |
                                                   v
                                                   Return Trade(cancelled state), Position (updated)



3. Done For Day
TradeOrder Request

       |        - >      Fail action if status is settled/cancelled
       v
 Check Market Status (closed/open)
       |
       v
 OPEN --> return Trade
       |
       v
 CLOSED --> return Trade(DFD status)










```
