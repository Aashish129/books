Script name:
1. kubectlResourceUsage.sh 
    - 
    - To capture the CPU and Memory metrics of the PODS and write to a file
    - command to run Script 
        - ./kubectlResourceUsage.sh | tee _filename_.txt
        - Ex: ./kubectlResourceUsage.sh | tee 180124-TestPods1000.txt
   - Example: Data Captured 
     - | NAME                                    | CPU(cores) |  MEMORY(bytes) |
        -----------------------------------------|------------|----------------|
       | apigateway-anm-6977bf89b4-5zlxd         | 1m         |  612Mi         |
       | apigateway-apimgr-58b97f5b84-ngr7v      |11m         | 1654Mi         |
       | apigateway-apitraffic-7d47787f47-2rnp6  | 6m         |  923Mi         |
       | apigateway-apitraffic-7d47787f47-mhf8p  | 6m         |  926Mi         |
       | apigateway-apitraffic-7d47787f47-mvr9b  | 7m         |  900Mi         |
     - apigateway-anm -> API Gateway Manager POD
     - apigateway-apimgr -> API Manager POD
     - apigateway-apitraffic -> API Gateway Traffic PODS
2. WriteMetrics.sh
   - To capture the CPU and Memory metrics and write to a file for the below:
     - The PODS on namespaces - Application & Add-ons
     - The Nodes
   - To keep monitoring and write the POD status to a file
   - command to run Script
       - ./WriteMetrics.sh <_Date_> <_ThreadCount_> <_TPSCount_>
       - Ex1: ./WriteMetrics.sh 12June 100 Full
       - Ex2: ./WriteMetrics.sh 12-06-2024 50 300
   - This will create 3 files as below:
       - [12June-100-Thread-Cloud-POD-Resource-Full-TPS.txt](Sample%20files%2F12June-100-Thread-Cloud-POD-Resource-Full-TPS.txt)
       - [12June-100-Thread-Cloud-POD_Status-Full-TPS.txt](Sample%20files%2F12June-100-Thread-Cloud-POD_Status-Full-TPS.txt)
       - [12June-100-Thread-Cloud-NodeInfo-Full-TPS.txt](Sample%20files%2F12June-100-Thread-Cloud-NodeInfo-Full-TPS.txt)
   - Dependency Files:
     - [kubectlResourceUsage.sh](kubectlResourceUsage.sh)
     - [kubectlPODRestart.sh](kubectlPODRestart.sh)
     - [kubectlResourceUsageNodes.sh](kubectlResourceUsageNodes.sh)
3. grepfile.sh
   - To Filter the APIGateway Manager, Gateway & Traffic pods CPU and Memory metrics and remove the suffix m & Mi to make to it easy to plot graphs
   - command to run Script
       - ./grepfile.sh <_Filename of POD Resource Metrics_>
       - Ex1: ./grepfile.sh 12June-100-Thread-Cloud-POD-Resource-Full-TPS.txt
   - This will create the below file:
     - [GrepData.txt](Sample%20files%2FGrepData.txt)
