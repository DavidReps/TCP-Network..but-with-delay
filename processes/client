package main

import (
	"../config"
	"../message"
	"bufio"
	"fmt"
	"math/rand"
	"net"
	"os"
	"strconv"
	"strings"
	"time"
)

type confile = config.Config
type Message = message.Message

//function that prints the email on the client side
func printMessage(ID int, message Message) {
	fmt.Println("\n ---------------------------- \n ---Message Confirmed Sent--- \n ---------------------------- \n")
	fmt.Println("Message Sent to process:" + strconv.Itoa(ID))
	fmt.Println("Message Content: " + message.Content)
	fmt.Println("Confirmed sent at: " + message.Time)
	fmt.Println("\n --------------------------- \n")
}

func UnicastSend(conn net.Conn, m Message) {
	//call delay to waste some time

	//actually send the message
	fmt.Fprintf(conn, m.Content+"\n")
	m.Time = time.Now().Format(time.RFC850)

	//print message client side with time stamp
	printMessage(m.Local_ID, m)
}

func delay(c confile){
	max := c.MaxD
	min := c.MinD
	//add timer to elapse a duration
	//call
	n := rand.Intn(max - min) + min
	ticker := time.NewTicker(time.Duration(n) * time.Millisecond)
	<- ticker.C
	ticker.Stop()
}

//will extract the message itself from command line
func MessageParse(text string) string{

	//create a string array to then parse out the message from the ID and IP info
	input := strings.Split(text, " ")

	//extract text after declarations
	MessageActual := input[2:]

	//convert the array to a simple string
	text = strings.Join(MessageActual, " ")

	return text

}



func main() {
	var c confile
	var m Message

	//read config file
	c = (config.ReadFile("config.txt"))[1]

	//create TCP channel
	address := c.IP + ":" + c.Port
	conn, err := net.Dial("tcp", address)
	if err != nil {
		panic(err)
	}

	defer conn.Close()
	for {
		//read command line prompt
		reader := bufio.NewReader(os.Stdin)
		fmt.Print("Please enter your Message:")

		//convert text to a string
		text, _ := reader.ReadString('\n')

		//extract only the message from the command line
		m.Content = MessageParse(text)
		m.Local_ID = c.ID

		if strings.TrimSpace(m.Content) != "END" {
			//add delay before sending
			delay(c)

			//send the message
			UnicastSend(conn, m)

			//end communication
		} else if strings.TrimSpace(m.Content) == "END"{
			UnicastSend(conn, m)
			fmt.Println("Exiting TCP Client")
			return
		}

	}

}
