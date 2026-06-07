---
layout: post
title: Log4j, Tomcat, and Family Campfires
date: 2006-03-10 11:51:25.000000000 -08:00
published: true
categories:
- Life in General
tags: []
permalink: "/2006/03/10/log4j-tomcat-and-family-campfires/"
---

First, the family campfires bit...

We have an AMAZING house that God has blessed us with, and with it a really nice back yard. And we have TONS of trees all throughout our property (note to self: take pictures of house and back yard for our little viewers). Well, as happens in a forest (that'd be where we live, complete with deer, bears, and coyotes), trees fall over (even when we're not there to hear them fall), and quite a few of the little guys have fallen in our yard.

I'd like to burn them, for the following noble reasons:

- To honor the fallen tree-warriors (okay, well, it sounds good)
- To serve as a warning to other trees as what will happen if they let their guard down and fall over in my yard (humor, folks)
- To clean up my yard (did I mention we have LOTS of fallen trees in our yard?)
- To roast marshmallows, hot dogs, and whatever else we can fit on a stick (wait a second, kids, get the cat off that stick...)
- To tell ghostly, ooky spooky stories!!!

In general, I think it will be a totally cool and neato thing to be able to have camp fires in our back yard. I am looking WAY forward to being able to do it!!! If I'm lucky, one of my clever little progeny will remember to take pictures too. =:)

Now, on to the log4j and tomcat thing...

I've spent the better part of yesterday beating my head against the wall, trying to get some servlets at work to log to their own logfiles using log4j and tomcat 5.5.x. It used to be a piece of cake to do this with tomcat 4, since tomcat 4 provided a nice Logger stanza for a given Servlet in its context.xml. But tomcat 5.5 changed all that.

I first tried to override log4j's rootLogger in each of my servlets in the tomcat container, and change this at run-time by using ${LOGNAME} in my log4j.properties and call System.setProperty() for LOGNAME at initialization time. This did not work and I have several bumps on my forehead to prove it.

So, today, after a good night sleep, I approached it differently--namely, by doing all the magic in 2 places...

log4j.properties now has a definition for each context (entry point--be it Servlet's init() or standalone class with a main()) that defines logfiles, formats, sizes, etc. It looks like this:

> # Root Logger definition. # this is where everything will go unless another logger is specified for itlog4j.rootLogger=INFO, R log4j.appender.R=org.apache.log4j.RollingFileAppender log4j.appender.R.File=${catalina.home}/logs/tomcat.log log4j.appender.R.MaxFileSize=10MB log4j.appender.R.MaxBackupIndex=10 log4j.appender.R.layout=org.apache.log4j.PatternLayout log4j.appender.R.layout.ConversionPattern=%-5p %d : %C{1}.%M : %m%n
>
>
> # Suppress the tomcat logging whilst DEBUG is switched on log4j.logger.org.apache.catalina.core=ERROR log4j.logger.org.apache.catalina.session=ERROR log4j.logger.org.apache.jasper.compiler=ERROR
>
>
> # our servlets... # we want these to go to different files, underneath tomcat's logs directory
>
>
> # Test Servlet log4j.logger.TestServlet=DEBUG, TS log4j.additivity.TestServlet=false log4j.appender.TS=org.apache.log4j.RollingFileAppender log4j.appender.TS.File=${catalina.home}/logs/TestServlet.log log4j.appender.TS.MaxFileSize=10MB log4j.appender.TS.MaxBackupIndex=10 log4j.appender.TS.layout=org.apache.log4j.PatternLayout log4j.appender.TS.layout.ConversionPattern=%-5p %d : %C{1}.%M : %m%n
>
>
> # PosInSpeedControlServlet log4j.logger.PosInSpeedControlServlet=DEBUG, PISCS log4j.additivity.PosInSpeedControlServlet=false log4j.appender.PISCS=org.apache.log4j.RollingFileAppender log4j.appender.PISCS.File=${catalina.home}/logs/PosInSpeedControlServlet.log log4j.appender.PISCS.MaxFileSize=10MB log4j.appender.PISCS.MaxBackupIndex=10 log4j.appender.PISCS.layout=org.apache.log4j.PatternLayout log4j.appender.PISCS.layout.ConversionPattern=%-5p %d : %C{1}.%M : %m%n
>
>
> # PosOutSimulatorServlet log4j.logger.PosOutSimulatorServlet=DEBUG, POSS log4j.additivity.PosOutSimulatorServlet=false log4j.appender.POSS=org.apache.log4j.RollingFileAppender log4j.appender.POSS.File=${catalina.home}/logs/PosOutSimulatorServlet.log log4j.appender.POSS.MaxFileSize=10MB log4j.appender.POSS.MaxBackupIndex=10 log4j.appender.POSS.layout=org.apache.log4j.PatternLayout log4j.appender.POSS.layout.ConversionPattern=%-5p %d : %C{1}.%M : %m%n

This seems to be doing the trick nicely, and it sure feels a whole lot cleaner. In addition, inside each entry point (Servlet.init() or Class.main()), I have the following code:

> DaLog.getInstance().initialize("TestServlet");

This allows DaLog (my little logger helper Singleton class) to send all logging information to the desired context in log4j. "TestServlet" above matches up nicely with the definition in my log4j.properties file " log4j.logger.TestServlet=DEBUG, TS". This ties the two pieces together a little more tightly than I'd like, but it sure feels a whole lot better than trying to kludge it another way. Here's my little DaLog class...

> package nft.util;
>
>
> import java.io.FileDescriptor; import java.io.FileOutputStream; import java.io.PrintStream;
>
>
> import org.apache.log4j.*;
>
>
> public class DaLog {
>
>
> private static String DEFAULTCONTEXT = "DEFAULT";
>
>
> private String _context = DEFAULTCONTEXT;
>
>
> private static DaLog _me;
>
>
> private PrintStream _realErr; private PrintStream _realOut;
>
>
> public static DaLog getInstance() { if (null == _me) _me = new DaLog();
>
>
> return _me; }
>
>
> private DaLog() { // save off references to "real" stderr and stdout... _realErr = new PrintStream(new FileOutputStream(FileDescriptor.err)); _realOut = new PrintStream(new FileOutputStream(FileDescriptor.out)); }
>
>
> /** * Initialize must be called once per instantiation of this class. The context * that is passed will be used as the context in the log4j.properties * file. This context is used to determine debug level, logfile location, * and other useful things. * @param context */ public void initialize(String context) {
>
>
> _context = context;
>
>
> restoreDefaultOutput();
>
>
> // make sure everything sent to System.err is logged System.setErr(new PrintStream(new LoggingOutputStream(Logger .getLogger(_context), Level.WARN), true));
>
>
> // make sure everything sent to System.out is also logged System.setOut(new PrintStream(new LoggingOutputStream(Logger .getLogger(_context), Level.INFO), true));
>
>
> }
>
>
> public Logger getLog() { return Logger.getLogger(_context); }
>
>
> public void shutdown() { restoreDefaultOutput(); }
>
>
> private void restoreDefaultOutput() { // restore stdout and stderr... System.setErr(_realErr); System.setOut(_realOut); }
>
>
> }

Now, if you, dear reader, have either been helped by this or know of a better way, PLEASE, PLEASE, PLEASE add a comment to this post and let me know!! =:) I was absolutely flabbergasted to find (or actually, to not find) yesterday that there were no complete examples of how to have more than one servlet using log4j in a container like Tomcat and going to different log files. Gah!!
