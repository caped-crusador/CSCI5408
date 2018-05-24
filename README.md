# CSCI5408
## Assignment 1
### Task: To perform EalsticSearch on the Bus data of the Municipality of Halifax. 
In order to get started with this task, first of all we need to install the necessary packages and tools on the system.
Elastic search needs Java to perform its tasks, we neeed to add the rpository and install java on the system.

Open your terminal and type the follwing commands

'''sudo add-apt-repository -y ppa:webupd8team/java'''
'''sudo apt-get update'''

_sudo apt-get -y install oracle-java8-installer_

Download and install the Public Signing Key:

_wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -_

Save the repository definition to /etc/apt/sources.list.d/elasticsearch-6.x.list:

_echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list_

Run apt-get update and the repository is ready for use. You can install it with:

_sudo apt-get update && sudo apt-get install elasticsearch_

