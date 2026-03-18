**Every car uses canbus.**

- Serial Communication
- Bus Interface
![[Pasted image 20240402163346.png]]
- Half duplex: Only one device can talk at a time.
- Differential Signal
	- More reliable
- Asynchronous
	- Doesn't use a shared clock source

Canbus connects ECU (Electrical Control Units).
Canbus allows any ECU to communicate over a CAN interface

## History
Before CANBus, 
BOSH released CAN in the 90s, and it became an international standard in '93.
Every car uses CANbus. 



## OS Tools and Commands

`ip link show`- list network devices including CAN
`candump canxxx` - dump the comms coming from interface canxx



---

# **CAN Bus Drop Length (Stub Length)**

  

## **Definition**

  

**CAN bus drop length** (also called _stub length_) is the short branch cable that connects a node (ECU, sensor, controller, etc.) to the main CAN backbone.

  

It is part of the **physical layer architecture** of a CAN network.

  

Drop length is **not** the total bus length — it is only the small branch from the main trunk to a device.

---

## **CAN Bus Physical Architecture**

  

A proper high-speed CAN network uses a **linear backbone topology**:

```
[120Ω]───Main Backbone────────Main Backbone────────[120Ω]
             |                        |
           Stub                     Stub
           (short)                  (short)
             |                        |
           Node                     Node
```

### **Key Rules**

- One continuous **twisted-pair backbone**
    
- Short **drop lines (stubs)** to each node
    
- **120Ω termination resistors only at the two ends**
    
- No star topology for high-speed CAN
    

---

## **Why Drop Length Matters**

  

CAN is a high-speed differential communication system.

  

If the stub is too long, it can cause:

- Signal reflections
    
- Ringing
    
- Data corruption
    
- Intermittent CAN errors
    
- Reduced maximum reliable bitrate
    

  

Long stubs act like transmission lines and cause impedance mismatch.

---

## **Recommended Maximum Stub Lengths (High-Speed CAN – ISO 11898-2)**

|**Bitrate**|**Max Stub Length**|
|---|---|
|1 Mbps|~0.3 m (30 cm)|
|500 kbps|~0.6 m|
|250 kbps|~1 m|
|125 kbps|~2 m|

### **Rule of Thumb**

  

Higher bitrate → shorter allowable stub length.

---

## **What NOT To Do (Star Topology)**

```
          Node
            |
Node --- Node --- Node
            |
          Node
```

Star configurations cause reflections and are not suitable for high-speed CAN.

---

## **Best Practice Summary**

- Keep the **backbone long**
    
- Keep the **drops short**
    
- Terminate only at the two physical ends
    
- Use proper twisted pair cable
    
- Match bitrate to total network length
    

---

If needed, calculate limits based on:

- Bitrate
    
- Total backbone length
    
- Number of nodes