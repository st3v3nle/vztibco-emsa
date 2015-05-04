# Tibco EMS Appliance Evaluation

## Setup Layout
We separated our boxes below:

* 5 client boxes 10.97.132.x [x => 191->195]
* 10.97.132.191: Grafana, InfluxDB and Consumers
* 10.97.132.[192-193]: Producers
* 10.97.132.[194-195]: Consumers
* 10.97.132.[186-197]: Tibco EMS Appliances FT Pair `Port: 9606`
* DR with 4 EMS Appliances
	
## Setup EMS Appliances
* Set up Failover Through Console
* Set up DR Through Console
* Upgrade EMS Appliances Through Console

##Single Store
**A single queue with own store**  

+ Throughput: `9.8K/sec`  
+ Max Latency: `750ms`  
+ Duration: `6h`

##Two Stores
**Two queues. Each has its own store**  

+ Total Throughput: `14K/sec`  
+ Per Queue Throughtput: `7K/sec`  
+ Max Latency: `750ms`   
+ Duration: `6h`

## Simulating Database Load
In our tests, we simulate Database Load randomly for every `15 minutes` with two queues. Each queue has its own store. We keep pumping messages constantly to reach EMS Appliance capacity.  
 
+ Throughput per queue: `4.5K/sec -> 6.4K/sec`  
+ Drain time: `2 Million` messages pending took `20-30 minutes` to drain

## Failover No Load
In this particular test, we starts with 2 Million messages pending, 2K message size  

### Hard Failover
**Procedure**: We unplug the cable of the EMS Appliance primary and watching the failover time and secondary recovery data duration. 

Steps: 

1. Unplug the cable from the primary  
2. Waiting for the failover  
3. Capture data from the logs, Grafana graphing and pending message size


### Soft Failover
**Procedure**: We manually stop the EMS instances to fail back  

### Result Summary

* Failover Fully Sync Time: `60 secs`
* Failover Secondary becomes Active: `15-45 secs`
* Failover Fully Consumers/Producers in service: `10-25 secs`	


## Failover with High Load
In this particular test with 14K messages/sec constantly into 2 queues that have their own store

### Hard Failover
**Procedure**: We unplug the cable of the EMS Appliance primary and watching the failover time and secondary recovery data duration. 

Steps: 

1. Put 2 Million Messages into 2 queues
2. Unplug the cable from the primary  
3. Waiting for the failover  
4. Capture data from the logs, grafana graphing and pending message size

### Soft Failover
**Procedure**: We manually stop the EMS instances to fail back

### Result Summary

* Failover Fully Sync Time: `60-104 secs`
* Failover Secondary becomes Active: `30-60 secs`
* Failover Fully Consumers/Producers in service: `20-35 secs`
* Queue Drains: `20 - 30 minutes`

## Disaster Recovery
Note: Due to the time contrainst, we only cover basic DR failover test with EMS Appliances in Tibco Labs. 


		
		