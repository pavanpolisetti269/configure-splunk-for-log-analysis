# configure-splunk-for-log-analysis
# Configuration Steps Universal Forwarder side:
## Install Splunk Universal Forwarder (Kali Linux) :
### 1.Download the Splunk Universal Forwarder:
#### * To install command splunk forwarder:
    sudo wget -O splunkforwarder-9.2.2-d76edf6f0a15-linux-2.6-amd64.deb https://download.splunk.com/products/universalforwarder/releases/9.2.2/linux/splunkforwarder-9.2.2-d76edf6f0a15-linux-2.6-amd64.deb

### 2.Install the Forwarder:
    tar -xvzf splunkforwarder-9.0.4-<architecture>.tgz
#### Here’s what each part of the command does:
* tar: The command to manipulate tar archives.
* -x: Extract the files from the archive.
* -v: Verbosely list files processed (optional, but helpful to see what is being extracted).
* -z: Filter the archive through gzip.
* f: Use the archive file.

### 3.To start the Splunk Universal Forwarder on Kali Linux:
 you need to navigate to the Splunk Forwarder directory and then execute the start command. Here's how you can do it:
#### 1.	Ensure you have extracted the tarball to /opt
#### 2.	Navigate to the Splunk Forwarder bin directory:
    cd /opt/splunkforwarder/bin/
#### 3. Start the Splunk Forwarder:
    sudo ./splunk start or status or restart
    
### 4.Configure the Forwarder:

#### 1.Connect splunk_forwarder to splunk_enterprise:
    /opt/splunkforwarder/bin/ ./splunk add forwarder-server [ip address of splunk_enterprise] : [port number to receive log through]                                                                                                                              

#### 2.Inputs.conf:
#### Navigate to the directory: 
    /opt/splunkforwarder/etc/system/local/inputs.conf 
#### Configure the any specific directory to analyse the logs
    [monitor:///var/log]
    sourcetype = syslog
    index= default/main
* This example monitors /var/log and assigns a syslog sourcetype.

#### 3.outputs.conf
#### Navigate to the directory: 
    /opt/splunkforwarder/etc/system/local/outputs.conf 
#### Purpose of output.conf
The output.conf file defines settings for sending data to different destinations, such as forwarding data to another Splunk instance, saving data to files, or sending data to third-party systems. It specifies how indexed data should be outputted after it has been processed by the Splunk indexer.

#### defaultGroup Directive:
    [defaultGroup]
    disabled = false
    index = default/main
* This configuration specifies that by default, indexed data should be sent to the default index.

#### tcpout and tcpout: Directives:
Configure settings for forwarding data over TCP to remote Splunk instances or other TCP receivers.
#### Example:
    [tcpout]
    defaultGroup = default_tcp_group
    [tcpout:default_tcp_group]
    server = [ip_address/splunk.example.com]:9997
* This configuration sets up Splunk to forward data to a remote Splunk indexer (splunk.example.com) on port 9997.
### 4.Start the Forwarder:
    sudo /opt/splunkforwarder/bin/splunk start
