#Flume

Source - netcat, sink - logger, channel - memory

# sample.conf: A single-node Flume configuration

# Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = netcat
a1.sources.r1.bind = localhost
a1.sources.r1.port = 44444

# Describe the sink
a1.sinks.k1.type = logger

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1

flume-ng agent --name a1 \
--conf /home/gnanaprakasam/flume/conf \
--conf-file /home/gnanaprakasam/flume/conf/sample.conf

telnet localhost 44444
nc localhost 44444

hdfs location for cloudera
hdfs://quickstart.cloudera:8020/user/cloudera/flume

hdfs locatino for itversity
hdfs://nn01.itversity.com:8020/user/gnanaprakasam/flume

Source - netcat, sink - hdfs, channel - memory

#Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

#Describe/configure the source
a1.sources.r1.type = netcat
a1.sources.r1.bind = localhost
a1.sources.r1.port = 44444

#Describe the sink
a1.sinks.k1.type = hdfs
a1.sinks.k1.hdfs.path = hdfs://nn01.itversity.com:8020/user/gnanaprakasam/flume
a1.sinks.k1.hdfs.filePrefix = events
a1.sinks.k1.hdfs.fileType = DataStream


#Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

#Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channels = c1


flume-ng agent --name a1 \
  --conf /home/gnanaprakasam/flume/conf \
  --conf-file /home/gnanaprakasam/flume/conf/example.conf

source - exec, sink - hdfs, channel - file

# Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = exec
a1.sources.r1.command = tail -F /opt/gen_logs/logs/access.log

# Describe the sink
a1.sinks.k1.type = hdfs
a1.sinks.k1.hdfs.path = /user/gnanaprakasam/flume/%y-%m-%d/%H%M/%S
a1.sinks.k1.hdfs.filePrefix = events-
a1.sinks.k1.hdfs.fileType = DataStream
a1.sinks.k1.hdfs.useLocalTimeStamp = true


# Use a channel which buffers events in memory
a1.channels.c1.type = FILE
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1

flume-ng agent --name a1 \
--conf /home/gnanaprakasam/flume/conf \
--conf-file /home/gnanaprakasam/flume/conf/source.conf
