# Route Configuration

This repository is a lab for NCTU course "Introduction to Computer Networks 2018".

---
## Abstract

In this lab, we are going to write a Python program with Ryu SDN framework to build a simple software-defined network and compare the different between two forwarding rules.

---
## Objectives

1. Learn how to build a simple software-defined networking with Ryu SDN framework
2. Learn how to add forwarding rule into each OpenFlow switch

---
## Execution

### How to run the program?
Note: This guide assumes you already have all the required programs and libraries installed. If not, you may log in to the provided container with "ssh –p <LAST_5_DIGITS_OF_STUDENT_ID> root@140.113.195.69" and password "cn2018"(assuming that you are using Linux like me).

  * Clone the repository
  ```
git clone https://github.com/nctucn/lab3-<GITHUB_ID>.git Route_Configuration 
```
  * Start the service of Open vSwitch
  ```
  service openvswitch-switch start
  ```
  * Open another terminal
  (Log in to the container if you need to)
  * Run the desired topology in one terminal **first**
  In the directory ```~/Route_Configuration/src```
  ```
  mn --custom <DESIRED_TOPO>.py --topo topo --link tc --controller remote
```
  * Run the desired CONTROLLER in another terminal
  In the directory ```~/Route_Configuration/src```
  ```
  ryu-manager <DESIRED_CONTROLLER>.py --observe-links
``` 
  * Test the performance with the following iPerf commands in the mininet (first) terminal. Replace <RESULT> with the desired name of the report.
  ```
   mininet> h1 iperf -s -u -i 1 –p 5566 > ./out/<RESULT> &
   mininet> h2 iperf -c 10.0.0.1 -u –i 1 –p 5566
``` 
  * You may check and compare the results in the ```Route_Configuration/src/out```

### Notes
#### How to traverse across the directories in the (Linux) terminal
  * Use ```cd``` to change current working directory
  * Use ```ls``` to list all files in the current working directory
  * use ```cd ..``` to return to a higher level directory or use ```cd ~``` to go to the root directory
  * Use ```less``` or ```cat``` to read the contents of a file
  * Use ```vim``` or ```nano``` should you ever need to edit a file
  
#### How to run mininet?
  * Use ```mn``` to run mininet
  * Use ```exit``` to exit mininet
  * Use ```mn -c``` after exiting to do a clean up
  
#### What to do if mininet crashes?
  * Use ```mn -c``` to do a clean up

#### How to exit the controller program?
  * Use ~Ctrl+Z~ to leave the mininet CLI
  * Use ```mn -c``` after exiting to do a clean up

### What is the meaning of the executing command (both Mininet and Ryu controller)?
  * Mininet: ```mn --custom <DESIRED_TOPO>.py --topo topo --link tc --controller remote```
    * *mn*: Run mininet
    * *custom*: Use the custom mininet file provided (<DESIRED_TOPO>.py)
    * *topo*: Indicates the topology to be used. Points to the topology defined in <DESIRED_TOPO>.py in this case
    * *link*: Specifies the type of link to be used (TCLink in this case)
    * *controller*: Specifies controller to be used. In this case, we are using a remote controller, which is the custom controller that we will be running with Ryu in another terminal, hence it being remote
  * Ryu Controller: ```ryu-manager <DESIRED_CONTROLLER>.py --observe-links```
    * *ryu-manager*: Runs the ryu-manager with <DESIRED_CONTROLLER>.py as the controller
    * *observe-links*: This option will turn on the topology RYU app, which will print out the links in the mininet
    
### Show the screenshot of using iPerf command in Mininet (both `SimpleController.py` and `controller.py`)
* SimpleController.py   
![Simple Controller](simplecon.png)
   
* controller.py   
![Edited Controller](controller.png)
---
## Description

### Tasks

> TODO:
> * Describe how you finish this work in detail

1. Environment Setup

2. Example of Ryu SDN

3. Mininet Topology

4. Ryu Controller

5. Measurement

### Discussion

> TODO:
> * Answer the following questions

1. Describe the difference between packet-in and packet-out in detail.
   
2. What is “table-miss” in SDN?
   
3. Why is "`(app_manager.RyuApp)`" adding after the declaration of class in `controller.py`?
   
4. Explain the following code in `controller.py`.
    ```python
    @set_ev_cls(ofp_event.EventOFPPacketIn, CONFIG_DISPATCHER)
    ```

5. What is the meaning of “datapath” in `controller.py`?
   
6. Why need to set "`ip_proto=17`" in the flow entry?
   
7. Compare the differences between the iPerf results of `SimpleController.py` and `controller.py` in detail.
   
8. Which forwarding rule is better? Why?

---
## References

> TODO: 
> * Please add your references in the following

* **Ryu SDN**
    * [Ryubook Documentation](https://osrg.github.io/ryu-book/en/html/)
    * [Ryubook [PDF]](https://osrg.github.io/ryu-book/en/Ryubook.pdf)
    * [Ryu 4.30 Documentation](https://github.com/mininet/mininet/wiki/Introduction-to-Mininet)
    * [Ryu Controller Tutorial](http://sdnhub.org/tutorials/ryu/)
    * [OpenFlow 1.3 Switch Specification](https://www.opennetworking.org/wp-content/uploads/2014/10/openflow-spec-v1.3.0.pdf)
    * [Ryubook 說明文件](https://osrg.github.io/ryu-book/zh_tw/html/)
    * [GitHub - Ryu Controller 教學專案](https://github.com/OSE-Lab/Learning-SDN/blob/master/Controller/Ryu/README.md)
    * [Ryu SDN 指南 – Pengfei Ni](https://feisky.gitbooks.io/sdn/sdn/ryu.html)
    * [OpenFlow 通訊協定](https://osrg.github.io/ryu-book/zh_tw/html/openflow_protocol.html)
* **Mininet**
    * [Mininet Walkthrough](http://mininet.org/walkthrough/)
* **Others**
    * [Markdown Tutorial](https://guides.github.com/features/mastering-markdown/)
    * [Vim Cheatsheet](https://www.maketecheasier.com/vim-keyboard-shortcuts-cheatsheet/)

---
## Contributors

* [Samson Choo](https://github.com/SamsonChoo)
* [David Lu](https://github.com/yungshenglu)

---
## License

GNU GENERAL PUBLIC LICENSE Version 3
