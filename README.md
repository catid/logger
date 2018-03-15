# logger
Feature-rich portable C++ logging subsystem in 650 lines of code

The library is self-contained and is easy to incorporate into iOS,
Android, Windows, Linux, and Mac projects.

Quick Start guide:

	// Example logging channel
	static logger::Channel Logger("Decoder", logger::Level::Debug);

	// Log out a message
	Logger.Info("Got first recovery packet: ColumnStart=",
		metadata.ColumnStart, " SumCount=", metadata.SumCount);


After trying several open-source loggers I ended up writing my own.
I was mainly looking for a multithreaded logger supporting levels,
and found a lot of buggy software that was hard to use or missing features.

Primary Logger features:

* Automatic initialization and shutdown just like 'cout'.
* Low performance impact since the logging occurs on a background thread.
* Automatically flushes message queue on shutdown.  (And it isn't buggy.)

Additional extra features:

* Logging Channel objects to sort messages by subsystem.
* Logging Levels enabling runtime filtering of messages and faster offline analysis.
* Serialization overloads in application code via LogStringize() overrides.
* Supports runtime-configurable prefix tags for each Channel.

On Android it uses __android_log_print().
On other platforms it uses std::fwrite(stdout).
On Windows it also uses OutputDebugStringA().

Modify this function to change how it writes output:

	OutputWorker::Log()
