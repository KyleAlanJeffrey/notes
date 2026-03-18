After running sim:
- Transfer the build config to the actual simulation: Use ctrl-f5

## Some Datatypes
### Timers/SettleTimers

**TON**: Timer
Attributes:
- Q: This states whether a timer has finished
- IN: This tells the timer to start
These are used for needing do tasks that take a specific amount of time. In SRF, this would be purging an applicator for 5 seconds or so. 
```
TON timer.IN = 1;
if (timer.Q){
	// timer finished
}
// Update settings
TON(&timer);
```


## Help Articles
Alarms -> Predefined alarm behavior


## Profiling
You can profile a machine with Automation Studio to see the cpu load based on modules.

To do this open the profiler: Open->Profiler
![[Pasted image 20250724141041.png]]

Then follow the below guide to record
![[Pasted image 20250724141700.png]]
## Installation
Install 4.10 here ->  [https://www.br-automation.com/en-us/downloads/#categories=Software-1344987434933/Automation+Stud[…]344987435049/Automation+Studio+4.10-1622214236094](https://www.br-automation.com/en-us/downloads/#categories=Software-1344987434933/Automation+Studio-1344987435049/Automation+Studio+4.10-1622214236094)

![[Pasted image 20251103192221.png]]

Download everything suggested in tools > Upgrades

Also download MappCockpit. An error will popup saying `no arflatpv`