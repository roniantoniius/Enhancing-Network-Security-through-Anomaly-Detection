# Enhancing Network Security through Anomaly Detection
#### Network Anomaly Detection

![image](https://github.com/roniantoniius/Enhancing-Network-Security-through-Anomaly-Detection/assets/121453378/12860d3f-9310-4fcd-bba9-1cf5a114428f)
Image Source: Pexels.com


Business Understanding:
In this increasingly digital age, computer networks play a very important role in the daily operations of organisations. They not only enable fast and efficient communication, but also support a wide range of critical applications, from financial transactions to sensitive data storage. However, along with the development of technology, cybersecurity threats are also increasing. Sophisticated and hard-to-detect cyberattacks are becoming a serious problem faced by many organisations. These attacks can not only result in huge financial losses, but also damage an organisation's reputation, lower customer trust, and disrupt business operations.

Faced with this problem, a sophisticated and reliable network anomaly detection system is needed to identify suspicious activities and potentially harmful attacks. The objective of this project is to develop a detection system that uses Machine Learning techniques such as Isolation Forest or DBScan. These techniques were chosen for their ability to effectively detect anomalies even on complex and large datasets. By implementing this system, it is hoped that organisations can improve their network security, detect attacks early, and take the necessary precautions to avoid further losses.

Goal:
As the number of cyber-attacks becomes increasingly sophisticated and difficult to detect, which can result in significant financial and reputational losses for organisations. The goal of this project is to develop an effective network anomaly detection system to identify suspicious activities and attacks on networks using Machine Learning techniques, such as Isolation Forest or DBScan, in order to improve security and prevent further potential attacks.

Data Understanding:
The dataset used in this project is a dataset that simulates different types of attacks in a military network environment. This dataset creates an environment to collect raw TCP/IP data from the network by simulating a US Air Force LAN. This LAN is simulated like a real environment and flooded with various attacks.

A connection is a series of TCP packets starting and ending at a certain time duration, where data flows to and from the source IP address to the target IP address under a well-defined protocol. Each connection is labelled as normal or attack with one specific attack type. Each connection record consists of about 100 bytes.

For each TCP/IP connection, 41 quantitative and qualitative features of normal and attack data are obtained (3 qualitative features and 38 quantitative features). The class variable has two categories:
- Normal
- Anomalous
    
**📃 Data:**

| No. | Column                       | Description                                                                                 | Data Type |
|-----|------------------------------|---------------------------------------------------------------------------------------------|-----------|
| 1   | duration                     | Connection duration (in seconds)                                                            | int64     |
| 2   | protocol_type                | Protocol type used (e.g., TCP, UDP, ICMP)                                                   | object    |
| 3   | service                      | Service type at the destination of the connection (e.g., HTTP, FTP, SMTP)                   | object    |
| 4   | flag                         | Connection status (e.g., SF, S0, REJ)                                                       | object    |
| 5   | src_bytes                    | Bytes sent from source to destination                                                       | int64     |
| 6   | dst_bytes                    | Bytes sent from destination to source                                                       | int64     |
| 7   | land                         | Indicates if the connection has the same source and destination IP addresses                | int64     |
| 8   | wrong_fragment               | Number of wrong fragments                                                                   | int64     |
| 9   | urgent                       | Number of urgent packets                                                                    | int64     |
| 10  | hot                          | Number of "hot" events on the connection                                                    | int64     |
| 11  | num_failed_logins            | Number of failed login attempts                                                             | int64     |
| 12  | logged_in                    | Login status (1 if successful, 0 if not)                                                    | int64     |
| 13  | num_compromised              | Number of compromised events on the system                                                  | int64     |
| 14  | root_shell                   | Indicates if root shell is accessed (1 if yes, 0 if no)                                     | int64     |
| 15  | su_attempted                 | Number of super user attempts                                                               | int64     |
| 16  | num_root                     | Number of root accesses                                                                     | int64     |
| 17  | num_file_creations           | Number of file creations                                                                    | int64     |
| 18  | num_shells                   | Number of shell accesses                                                                    | int64     |
| 19  | num_access_files             | Number of access files                                                                      | int64     |
| 20  | num_outbound_cmds            | Number of outbound commands                                                                 | int64     |
| 21  | is_host_login                | Indicates if the login is from the host (1 if yes, 0 if no)                                 | int64     |
| 22  | is_guest_login               | Indicates if the login is as a guest (1 if yes, 0 if no)                                    | int64     |
| 23  | count                        | Number of connections to the same host in the last two seconds                              | int64     |
| 24  | srv_count                    | Number of connections to the same service in the last two seconds                           | int64     |
| 25  | serror_rate                  | Percentage of connections with SYN errors                                                   | float64   |
| 26  | srv_serror_rate              | Percentage of connections to the same service with SYN errors                               | float64   |
| 27  | rerror_rate                  | Percentage of connections with REJ errors                                                   | float64   |
| 28  | srv_rerror_rate              | Percentage of connections to the same service with REJ errors                               | float64   |
| 29  | same_srv_rate                | Percentage of connections to the same service                                               | float64   |
| 30  | diff_srv_rate                | Percentage of connections to different services                                             | float64   |
| 31  | srv_diff_host_rate           | Percentage of connections to different hosts on the same service                            | float64   |
| 32  | dst_host_count               | Number of connections to the destination host                                               | int64     |
| 33  | dst_host_srv_count           | Number of connections to the same service on the destination host                           | int64     |
| 34  | dst_host_same_srv_rate       | Percentage of connections to the same service on the destination host                       | float64   |
| 35  | dst_host_diff_srv_rate       | Percentage of connections to different services on the destination host                     | float64   |
| 36  | dst_host_same_src_port_rate  | Percentage of connections to the same service from the same source port                     | float64   |
| 37  | dst_host_srv_diff_host_rate  | Percentage of connections to different hosts on the same service on the destination host    | float64   |
| 38  | dst_host_serror_rate         | Percentage of connections to the destination host with SYN errors                           | float64   |
| 39  | dst_host_srv_serror_rate     | Percentage of connections to the same service on the destination host with SYN errors       | float64   |
| 40  | dst_host_rerror_rate         | Percentage of connections to the destination host with REJ errors                           | float64   |
| 41  | dst_host_srv_rerror_rate     | Percentage of connections to the same service on the destination host with REJ errors       | float64   |
| 42  | class                        | Connection class label (Normal or Anomalous)                                                | object    |

**Note:**
- TCP: Reliable data transmission protocol.
- UDP: Fast protocol without reliability guarantees.
- ICMP: Protocol for network error messages.
- HTTP: Protocol for accessing websites.
- FTP: Protocol for file transfer.
- SMTP: Protocol for sending emails.
- SF: Successful connection without errors.
- S0: Connection started but not completed.
- REJ: Connection rejected.
- Hot: Suspicious activity.
- Shell: Command line interface.
- SYN: Packet to initiate a connection.
- REJ: Connection or request rejected.


### Data Preprocessing

- missing value
- duplikat
- outlier
- numerik & kategorik & output
- EDA Numerik dan Kategorik
- feature engineering 
	- encoding 
	- scaling


### Modeling
- Modeling & Evaluation first
	- Extended Isolation Tree
	- DBSCAN
	- LocalOutlierFactor

- Feature Selection: Random Forest RFE
- Hyperparameter on EIF & LOF

### Evaluation
- Model Performance Evaluation
- Anomaly Detection Visualization Evaluation
  
![newplot](https://github.com/roniantoniius/Enhancing-Network-Security-through-Anomaly-Detection/assets/121453378/d1bd28e1-2c9b-4bc6-a655-c3e584012c8c)

![newplot_(1)](https://github.com/roniantoniius/Enhancing-Network-Security-through-Anomaly-Detection/assets/121453378/d37ee6b3-39a8-4fb4-b123-cbdf3782babe)


## Conclusion
The Extended Isolation Forest (EIF) model proves to be the best choice for this anomaly detection project. The EIF model was applied with 200 trees and a sample size of 64, and it effectively distinguished between normal and anomalous connections. The model achieved an accuracy of 86%, with a precision of 66% for anomalies and 87% for normal data on the test set. Additionally, the adjusted rand scores for the training and test sets are 0.223 and 0.228, respectively, further indicating the model's ability to correctly classify anomalies within the dataset. Thus, EIF stands out as the optimal model for this project due to its superior performance in identifying anomalies.

Visualisation of the 3D scatter plot of the t-SNE-applied X_test_rfe data and the prediction results using **iForest** shows that most of the normal data (marked in blue) is evenly distributed and well clustered, while the anomalous data (marked in red) is concentrated in a few discrete areas but almost all of the anomalous data is located when Z values are high and X and Y values are low (around 0), demonstrating the ability of the iForest model to detect anomalies that differ significantly from the normal pattern. Some anomalies are located far from the normal clusters, signalling clear and distinct anomalies, while some anomalies close to the normal data indicate challenges in classification.
