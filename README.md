# Starting up Grafana and using Graphyte

## Install Grafana
Download and install Grafana here: https://grafana.com/grafana/download
I wouldn't recommend using a Docker container for our purposes, as we need to allow unsanitised HTML in order to support video streaming. This is very difficult in a Docker container, as it requires accessing the initialization file. 

## Navigate to, or create, your custom ini 
Navigate to your installation of grafana, and edit the custom.ini or grafana.ini files. The filename differs between operating systems. 

###### Linux 
If you installed Grafana using the deb or rpm packages, then your configuration file is located at /etc/grafana/grafana.ini and a separate custom.ini is not used. This path is specified in the Grafana init.d script using --config file parameter

##### Windows
sample.ini is in the same directory as defaults.ini and contains all the settings commented out. Copy sample.ini and name it custom.ini

##### MacOS
By default, the configuration file is located at /usr/local/etc/grafana/grafana.ini. To configure Grafana, add a configuration file named custom.ini to the conf folder to override any of the settings defined in conf/defaults.ini.

## Allow unsanitized HTML
In the aforementioned file, find the line with disable_sanitize html in it. It will initially be commented out with ;. Modify it so that the line looks like this:

disable_sanitize_html = true

Now you can add HTML methods such as video streaming and tags.


# Graphyte example

Graphyte allows you to send data to Graphana's Carbon platform, directly in your python code. 

## Install
Graphyte is on PyPI so you can just use:
pip install graphyte

Remember to set up your virtual environment!

## Use
To use Graphyte, call init() to initialize the default sender and then send() to send a message. 
Ex: to send "system.sync.foo.bar 42 {timestamp}\n" to graphite.example.com:2003 synchronously:

import graphyte
graphyte.init('graphite.example.com', prefix='system.sync')
graphyte.send('foo.bar', 42)

When trying to send asynchronously change the prefix to reflect, and add interval that you want to send, as follows:

graphyte.init('graphite.example.com', prefix='system.async', interval=10)
graphyte.send('foo.bar', 42)




