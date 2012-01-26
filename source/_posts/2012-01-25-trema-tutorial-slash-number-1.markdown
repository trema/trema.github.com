---
layout: post
title: "Hello Trema! (Tutorial #1)"
date: 2012-01-25 16:42
comments: true
published: false
categories: 
---
{% blockquote Anonymous http://www.quotationspage.com/quote/790.html %}
Efficiency is intelligent laziness.
{% endblockquote %}

{% blockquote Larry Wall, Programming Perl %}
Laziness - The quality that makes you go to great effort to reduce
overall energy expenditure.
{% endblockquote %}


# Preface

<!-- 優れたプログラマが持つハッカー気質のひとつに「無精」があります。大
好きなコンピュータの前から一時も離れずにどうやってジャンクフードを手に
入れるか̶̶̶普通の人からするとただの横着に見えるかもしれませんが、ハッカー
達にとってそれはいつでも大きな問題でした。たとえば、ハッカーの巣窟とし
て有名な MIT のAI ラボにはかつて、UNIX のコマンド一発でピザを FAX 注文
する xpizza コマンドが存在しました (注1)。また、RFC 2325 として公開され
ているコーヒーポットプロトコルでは、遠隔地にあるコーヒーポットのコーヒー
の量を監視したり、コーヒーを自動的に淹れたりするための半分冗談のインター
フェースを定義しています。 -->

"Laziness" is one of the hackers' mentality that only excel
programmers possess. How he can get some junk food without leaving
from his lovable computer even for a second --- that may look lazy to
normal people, but that always been a really serious thing to
hackers. For example, at MIT AI laboratory, the famous den of hackers,
there existed a one-button-push Unix command called xpizza{% fn_ref 1 %}
to order pizza by fax. In addition, the coffee pot protocol
published as RFC 2325 defines a half-joking interface to remotely
control coffee pot in order to specify the amount of coffee or brew
coffee automatically.


<!-- こうした「ソフトウェアで楽をする」ハックのうち、もっとも大規模な例
が最新鋭の巨大データセンターです。クラウドサービスの裏で動く巨大データ
センターは極めて少人数の管理者によって運用されており、大部分の管理はソ
フトウェアによって極限まで自動化されているという記事を読んだことがある
人も多いでしょう。ピザやコーヒーのようなお遊びから、巨大データセンター
のように一筋縄ではいかない相手まで、プログラムで「モノ」を思いどおりに
コントロールするのはもっとも楽しいハックの一種です。-->

Such "software simplicity" was all done for hacker's sake. A much
bigger example is the state-of-the-art computer center.  Majority of
the management software aims towards automation and I think many
people would have read an article as such.  Shifting the focus from
pizza or coffee play arena to a large data center is not for the
faint-hearted but to control things by a program to one's discretion
would please even the most jaded hacker.


{% footnotes %}
  {% fn You can find the man page of xpizza (http://bit.ly/mYAJwZ) written in 1991 by googling with "xpizza MIT" for a keyword %}
{% endfootnotes%}


## Introduction to Openflow

In this article we attain a skill to hack a network called Openflow.

Openflow as defined in #2 is the protocol that modifies the internal behavior of a network switch. 

Using the software that controls the  switch (well-known as Openflow controller) we are aiming to programmatically control an entire network.

Up to now only trained operators managed networks but the introduction of Openflow made it possible for programmers too.

To automate a network capable of being able to optimize itself to application needs or self-recover from impairments is not a dream anymore!

In this article we use an Openflow controller to create a network and master the techniques of "hacking" it over several sections.

One of the frequently asked questions is "What can I do if I use Openflow?" And the short answer to this is.
Create a small to medium size network at the office or home that soon can be tested with easy understandable code.

I am going to explain the basics of Openflow networking in greater detail and build up a conceptual framework incrementally not only for the network specialists but to any generic programmer.

But first let's us introduce the Trema framework.

## Openflow programming framework Trema.

Trema is a programming framework that can be used for the development of an Openflow controller in Ruby as well as C.

If you ever wanted to do agile Openflow development on a single PC then look no further than Trema.

> Nick's pitch
> Instead of having to troubleshoot problems or experiment with settings Trema's Openflow programming framework gives you a stable environment with software that works. Simply put it it is a gold mine of ideas that work.

Trema is a public domain software found on GitHub licensed under GPLv2.

The software introduced formally to the world in April this year and although still in its infancy it has been quickly adopted by domestic and overseas universities and well as research institutions because of its simplicity.

Information about Trema can be found from the following sites:

 * Trema Home Page: http://trema.github.com/trema/
 * GitHub page: https://github.com/trema/
 * Mailing List: https://groups.google.com/group/trema-dev
 * Twitter account: @trema_news

Trema makes it possible to do Openflow controller development and testing on a single note PC.

In this article using the current Trema through experimentation I'll create an Openflow controller.

Well let's setup Trema and write a simple program.

## Setup

Trema runs on Ubuntu 10.04 or later, Debian GNU/Linux 6.0 on 32 or 64 bit versions flavors of Linux.
Although hasn't been tested it might work on other versions of Linux. 

In this article I use the latest Ubuntu 11.04 (desktop edition) 32-bit version.

To execute Trema commands root access required.

First please confirm the setup file of sudo by typing a command using sudo that requires root access.

    % sudo visudo

Once you have confirmed that can use sudo to run a command as superuser install Trema's other software dependencies like gcc by typing the following command:

    % sudo apt-get install git gcc make ruby ruby-dev libpcap-dev libsqlite3-dev

Next download Trema.

By using git obtain the latest version of the public available Trema software from GitHub.

    % git clone git://github.com/trema/trema.git

To setup Trema something like "make install" installation for the entire system is unnecessary. 
Just build and use immediately. To build just type the following command.

    % ./trema/build.rb

Well let's write our famous Hello Trema controller in Ruby.

In this article we use Trema's Ruby library to program.

For programming in C please refer to developed examples under the directory src/examples.

For all the Ruby code that will develop in this article you can find the equivalent C code.

## Hello Trema!

In the trema directory create a file hello_trema.rb and copy paste the context of listing 1 into it.

So let's try it out!

Use the trema run command to execute the controller code.
So let's output to the screen the world's smallest controller [Hello, Trema!]

    % cd trema
    % ./trema run ./hello_trema.rb
    Hello, Trema! <-- Press Ctrl-C to terminate

How about that?
I think you would agree with me that it was so easy to write and execute a Trema controller.

But wait? What happened to our control switch?

Although every piece of information is written in Trema about the controller it actually did nothing in particular noticeable.

But need to be more patient until we connect a switch.　But for now let's us first explain the source code in more detail.

## Controller class definition

If you code in Ruby every controller must be inherited from the Controller class (listing 1).
Sub-classing from the Controller class you also inherit controller's functionality.

## Handler definition

Trema is an event driven programmable model. 
In order words before the arrival of any Openflow message if you register a handler for a particular event your handler would be called once that event occurs.
For example if you define a start method the controller after start-up would automatically invoke it.
Fundamentally well that's all there is to Trema.

Next let's write a more practical controller without a connected switch and name it a monitoring switch.
Its purpose is to display in real-time running switches and detect those that crashed in a network.

## Switch Monitoring

Figure#2 depicts the operation of a switch monitor.

At start-up an Openflow switch would attempt to establish connection with the controller.

In Trema when a switch establishes connection the switch_ready handler is called.

Controller updates switch's list adding the most recent activated switch.

On the contrary if a switch for any reason is disconnected from the controller the switch_disconnected handler is called.
The controller modifies the list, by deleting the switch that went down.

## Virtual network

Let's us write some sample code that detects when a switch is up and running.
But how? 
Trema enables you to create code without any reference to an Openflow switch and further test it and execute it.
What does this means?
The answer to this is put down into one of Trema's most powerful feature - virtual network environment/prototype.
It facilitates a controller simulation environment comprising of a network of interconnected Openflow virtual switches and virtual hosts thus eliminating the need for physical switches and hosts.

Of course the developed controller would also work on the network consisting of physical Openflow switches and hosts with no additional effort whatsoever.
Well let's start and observe the virtual switch.

## Virtual Openflow switch start-up

To run a virtual switch invoke the trema run on a composed virtual network described by its setup file.

For example listing 2 shows a setup file defining 2 virtual switches.

    listing 2 Setup of 2 virtual switches in a virtual network
    vswitch { datapath_id 0xabc }
    vswitch { datapath_id 0xdef }

For each switch a datapath_id (0xabc, 0xedf) similar to a MAC address of a network card a unique ID to use is defined.

According to Openflow standard this is a 64-bit integer value assigned to each switch.
This number can be anything you like to be as long as it remains unique.

## Responding to switch's activation

Let's launch the switch as defined above and see how to respond to it from the controller.

We write a switch_ready handler to respond when switch goes up.
We define an instance variable @switches to store currently activated switch's datapath_id.
Also call the puts method to display the datapath_id.

## Responding to switch's disconnection.

In a similar fashion let's see how to respond to the event when a switch disconnects.
The handler this time is switch_disconnected (listing 3 ②)
When a switch disconnects remove its datapath_id from @switches and call the puts method to display it.

## List of switches

Lastly let's us display the switches using some fixed interval.
If you want some action to be invoked at fixed interval use a timer function.
As listing 3 ③ shows, use periodic_timer_event to register a callback to be called with a desired timer interval.
Then call the show_switches method every 10 seconds to display.

    listing 3 SwitchMonitor controller
   
    class SwitchMonitor < Controller
      periodic_timer_event :show_switches, 10 ③
      def start
        @switches = []
      end
      def switch_ready datapath_id ①
        @switches << datapath_id.to_hex
        info "Switch #{ datapath_id.to_hex } is UP"
      end
      def switch_disconnected datapath_id ②
        @switches -= [datapath_id.to_hex ]
        info "Switch #{ datapath_id.to_hex } is DOWN"
      end
      private ③
      def show_switches
        info "All switches = " + @switches.sort.join( ", " )
      end
    end


## Run
Let's quickly execute and observe the results.
For example to startup 3 virtual switches save the context of listing 4 into a file (switch-monitor.conf) and run it using trema run with the -c option supplied.

    %./trema run ./switch-monitor.rb -c ./switch-monitor.conf

When the switch-monitor controller is executed it reads the configuration file and starts the 3 virtual switches and for each the switch_ready handler invoked that displays this message.
Let's confirm the detection of switch's teardown.
To stop the switch use the trema kill command.

Using a different terminal type the following command to bring switch #3 down.

    ./trema kill 0x3

Returning back to the terminal window where the trema run command was executed you should see the following output:

    ./trema_run ./switch-monitor.rb -c ./switch-monitor.conf

    listing 4 Definition of 3 virtual switches
    vswitch { datapath_id 0x1 }
    vswitch { datapath_id 0x2 }
    vswitch { datapath_id 0x3 }

    Switch 0x3 is UP
    Switch 0x2 is UP
    Switch 0x01 is UP
    All switches = 0x1, 0x2, 0x3
    All switches = 0x1, 0x2, 0x3
    All switches = 0x1, 0x2, 0x3
    ...
    Switch 0x3 is DOWN

It worked as expected.

As you can see this message is displayed by the switch_disconnected handler.

## Conclusion

We wrote a Hello World that serves as a template for every controller. Also we created a switch monitor to observe the run state of the modeled switches.
What we have learned so far are the following three:

* In an Openflow network the controller software can be used to process packets from switches and control them.
Trema is the programmable framework for writing such controller software.

* Trema provides the ability to create a virtual network so even if you don't have access to an Openflow switch can develop and test.
For example in a virtual network can create a virtual switch and assign it any arbitrary datapath_id.

* A controller is a Ruby Controller class that can inherit any Openflow event through a corresponding defined handler to control any switch.
For example can write actions to respond to switch's startup and teardown by a switch_ready and switch_disconnected handlers.

Next we go beyond the typical controller and create a layer 2 switch traffic aggregation program.

I would implement a basic layer-2 switching function that accumulates and classifies traffic by user and volume.

    listing 1 Hello Trema! Controller
    class HelloController < Controller ---①
      def start ---②
        puts "Hello, Trema!"
      end
    end

    listing 2 Add 2 virtual switches in a virtual network
    vswitch { datapath_id 0xabc }
    vswitch { datapath_id 0xdef }

    listing 3 SwitchMonitor Controller
    class SwitchMonitor < Controller
      periodic_timer_event :show_switches, 10 ---③
      def start
        @switches = []
      end
      def switch_ready datapath_id ---①
        @switches << datapath_id.to_hex
        info "Switch #{ datapath_id.to_hex } is UP"
      end
      def switch_disconnected datapath_id ---②
        @switches -= [datapath_id.to_hex ]
        info "Switch #{ datapath_id.to_hex } is DOWN"
      end
      private ---③
      def show_switches
        info "All switches = " + @switches.sort.join( ", " )
      end
    end

### Youtarou column What is datapath?
Q. Hello! My name is Youtarou and I am the one with an interest in Openflow programming.
I understood that it is an ID attached to the switch but really what is datapath id? That switch?
A. From practical point of view it is not wrong to think that [datapath_id == Openflow switch]
A google search or a reference from hardware textbook reveals that [CPU performs arithmetic processing of instructions issued by a controller to the datapath.]
In general all hardware classify datapath to be the muscle and controller the brain. Similarly Openflow follows the same analogy.
The Openflow datapath deals with the packet processing of a denoted switch, and it is this control software that is called controller.

### Youtarou column what is switch_ready?
Q. Reading the Openflow specification can not find any reference to the word switch_ready. Is such event defined in Openflow?
A. switch_ready is Trema's original event dispatched to controller's class when a switch establishes connection with Trema.
Actually switch_ready as shown on the opposite sequence of events, Trema encapsulates well all the Openflow protocol details.
At first let's confirm the protocol conversation between the switch and the Openflow controller.
Next acquire switch's identity datapathID.
Then send a FeaturesRequest message to retrieve switch's characteristic information similar to datapathID.
If succeeded the datapathID and number of ports embedded into FeaturesReply message that is sent.
Finally we initialize the switch.
This is done to avoid conflict with any previous state information that a controller may had.
Once these sequence of events completed as expected notify the controller with a switch_ready.
