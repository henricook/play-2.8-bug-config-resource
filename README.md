# Bug demonstration

This repository is intended to demonstrate: https://github.com/playframework/playframework/issues/9972

I believe this issue has been introduced in Play 2.8.x and is a regression from Play 2.7.x - more info in the issue

# How to recreate

- Observe that conf/test.conf exists
- Run `sbt show runtime:fullClasspath` to verify that /conf is on the class path
- Run `sbt -Dconfig.resource test.conf` to start the shell with custom _config.resource_ parameter
- Run `;clean;run` - observe failure saying test.conf cannot be found:

```
[error] Configuration error: Configuration error[test.conf: java.io.IOException: resource not found on classpath: test.conf]
[error]         at play.api.Configuration$.configError(Configuration.scala:138)
[error]         at play.api.Configuration$.load(Configuration.scala:81)
[error]         at play.core.server.DevServerStart$.$anonfun$mainDev$1(DevServerStart.scala:230)
[error]         at play.utils.Threads$.withContextClassLoader(Threads.scala:21)
[error]         at play.core.server.DevServerStart$.mainDev(DevServerStart.scala:75)
[error]         at play.core.server.DevServerStart$.mainDevHttpMode(DevServerStart.scala:49)
[error]         at play.core.server.DevServerStart.mainDevHttpMode(DevServerStart.scala)
[error]         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
[error]         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
[error]         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
[error]         at java.lang.reflect.Method.invoke(Method.java:498)
[error]         at play.runsupport.Reloader$.startDevMode(Reloader.scala:306)
[error]         at play.sbt.run.PlayRun$.devModeServer$lzycompute$1(PlayRun.scala:98)
[error]         at play.sbt.run.PlayRun$.devModeServer$1(PlayRun.scala:81)
[error]         at play.sbt.run.PlayRun$.$anonfun$playRunTask$3(PlayRun.scala:105)
[error]         at play.sbt.run.PlayRun$.$anonfun$playRunTask$3$adapted(PlayRun.scala:67)
[error]         at scala.Function1.$anonfun$compose$1(Function1.scala:49)
[error] Caused by: com.typesafe.config.ConfigException$IO: test.conf: java.io.IOException: resource not found on classpath: test.conf
[error]         at com.typesafe.config.impl.Parseable.parseValue(Parseable.java:190)
[error]         at com.typesafe.config.impl.Parseable.parseValue(Parseable.java:174)
[error]         at com.typesafe.config.impl.Parseable.parse(Parseable.java:301)
[error]         at com.typesafe.config.ConfigFactory.parseResources(ConfigFactory.java:1058)
[error]         at com.typesafe.config.ConfigFactory.parseResources(ConfigFactory.java:986)
[error]         at com.typesafe.config.DefaultConfigLoadingStrategy.parseApplicationConfig(DefaultConfigLoadingStrategy.java:49)
[error]         at com.typesafe.config.ConfigFactory.defaultApplication(ConfigFactory.java:529)
[error]         at play.api.Configuration$.load(Configuration.scala:58)
[error]         at play.core.server.DevServerStart$.$anonfun$mainDev$1(DevServerStart.scala:230)
[error]         at play.utils.Threads$.withContextClassLoader(Threads.scala:21)
[error]         at play.core.server.DevServerStart$.mainDev(DevServerStart.scala:75)
[error]         at play.core.server.DevServerStart$.mainDevHttpMode(DevServerStart.scala:49)
[error]         at play.core.server.DevServerStart.mainDevHttpMode(DevServerStart.scala)
[error]         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
[error]         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
[error]         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
[error]         at java.lang.reflect.Method.invoke(Method.java:498)
[error]         at play.runsupport.Reloader$.startDevMode(Reloader.scala:306)
[error]         at play.sbt.run.PlayRun$.devModeServer$lzycompute$1(PlayRun.scala:98)
[error]         at play.sbt.run.PlayRun$.devModeServer$1(PlayRun.scala:81)
[error]         at play.sbt.run.PlayRun$.$anonfun$playRunTask$3(PlayRun.scala:105)
[error]         at play.sbt.run.PlayRun$.$anonfun$playRunTask$3$adapted(PlayRun.scala:67)
[error]         at scala.Function1.$anonfun$compose$1(Function1.scala:49)
[error] Caused by: java.io.IOException: resource not found on classpath: test.conf
[error]         at com.typesafe.config.impl.Parseable$ParseableResources.rawParseValue(Parseable.java:726)
[error]         at com.typesafe.config.impl.Parseable$ParseableResources.rawParseValue(Parseable.java:701)
[error]         at com.typesafe.config.impl.Parseable.parseValue(Parseable.java:180)
[error]         at com.typesafe.config.impl.Parseable.parseValue(Parseable.java:174)
[error]         at com.typesafe.config.impl.Parseable.parse(Parseable.java:301)
[error]         at com.typesafe.config.ConfigFactory.parseResources(ConfigFactory.java:1058)
[error]         at com.typesafe.config.ConfigFactory.parseResources(ConfigFactory.java:986)
[error]         at com.typesafe.config.DefaultConfigLoadingStrategy.parseApplicationConfig(DefaultConfigLoadingStrategy.java:49)
[error]         at com.typesafe.config.ConfigFactory.defaultApplication(ConfigFactory.java:529)
[error]         at play.api.Configuration$.load(Configuration.scala:58)
[error]         at play.core.server.DevServerStart$.$anonfun$mainDev$1(DevServerStart.scala:230)
[error]         at play.utils.Threads$.withContextClassLoader(Threads.scala:21)
[error]         at play.core.server.DevServerStart$.mainDev(DevServerStart.scala:75)
[error]         at play.core.server.DevServerStart$.mainDevHttpMode(DevServerStart.scala:49)
[error]         at play.core.server.DevServerStart.mainDevHttpMode(DevServerStart.scala)
[error]         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
[error]         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
[error]         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
[error]         at java.lang.reflect.Method.invoke(Method.java:498)
[error]         at play.runsupport.Reloader$.startDevMode(Reloader.scala:306)
[error]         at play.sbt.run.PlayRun$.devModeServer$lzycompute$1(PlayRun.scala:98)
[error]         at play.sbt.run.PlayRun$.devModeServer$1(PlayRun.scala:81)
[error]         at play.sbt.run.PlayRun$.$anonfun$playRunTask$3(PlayRun.scala:105)
[error]         at play.sbt.run.PlayRun$.$anonfun$playRunTask$3$adapted(PlayRun.scala:67)
[error]         at scala.Function1.$anonfun$compose$1(Function1.scala:49)
[error] stack trace is suppressed; run last Compile / run for the full output
[error] (Compile / run) java.lang.reflect.InvocationTargetException
```
