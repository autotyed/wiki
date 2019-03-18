Metrics collections is performed by Telegraf. This open source application runs
scripts that import data from various sources into InfluxDB. InfluxDB is a time
series database that stores metric data points. Glances is also used to collect
system metrics. This is one of the best (nearly only) way to collect system data
on a Mac for InfluxDB storage. All of these apps work wonderfully on Linux as well.

If you're using Ubiquiti UniFI devices on your network, you're strongly encouraged
to install and utilize unifi-poller. This application polls your Unifi controller
and stores the metrics in InfluxDB. The controller does not need to be running on
the same computer as unifi-poller, nor InfluxDB. They can all be separate systems
if that works for you.

Use the navigation menu (on the right) to learn more about each component.
