#TCP Network with added delay

Overview:

This program creates a TCP channel, only to simulate issues in the connection we have implemented a delay prior to
sending. Much like any TCP channel we have implemented a server as well as a client. The server's primary function is to
listen and receive messages from the client. Unique in our design is we implement a configuration file and reader. This
program's task is to read and consequently parse out relevant information from a standard text file and then populate
fields related to  the TCP channel's unique configuration. This  implementation allows us to be able to dynamically
create TCP channels in order to communicate over different ports with different individuals. Freedom to communicate
with only those whom you desire is a hallmark of any robust communication protocol. This design allows the user to only
communicate as they desire.

Functionality:

We define our message structure in a separate file and then import it so as to be able to access it from any file.
After the config file has been read it will then populate a structure with the information regarding ID's, IP's, Ports,
as well as the delay parameters. The TCP channels are then created after each file's execution. The client is then
prompted to write their message. The message contains the desired action (send), which ID will receive, as well as the
message itself. The message is then parsed to extracting only the message from the command line input. Once the
message itself is obtained it is then we call a delay function whose job is to waste time. This simulates an issue in
the system. After the delay the message is sent with a time stamp on both the client and server side. This is done
in the hopes that it may mitigate some issues caused by the delay, including but not limited to messages being delivered
out of order. The client is then prompted again to send a new message or end communication.

Usage:

In order to use this TCP channel open a command line and run the "go run server.go". The server is now running, at this
point you need to open a second command line and run "go run client.go". This command line will prompt you to enter your
message. Enter a message following the format "send, # of the ID, message content". To end the TCP channel replace the
message content with "END". This will exit the TCP client and server. We have allocated the client to ID # 1 and the
Server ID # 2
