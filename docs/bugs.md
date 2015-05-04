# Tibco Bugs

## Unable to load `destination_backlog_swapout` bug

If we set destination_backlog_swapout is over 1M in JSON config, Tibco Server will throw an FATAL error and reset the value to default value. 

## Unable to ACK messages in the failover test with `EXPLICIT_CLIENT_ACK` mode

1. Producers send with rate 7K messages/sec
2. Start Consumers only when we see 2M messages in the queue
3. Failover Primary -> Secondary
4. Unable to “ACK” messages. Except throws for invalid message


