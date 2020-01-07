# Bug demonstration

This repository is intended to demonstrate:

I believe this issue has been introduced in Play 2.8.x and is a regression from Play 2.7.x - more info in the issue

# How to recreate

- Observe that conf/test.conf exists
- Run `sbt show runtime:fullClasspath` to verify that /conf is on the class path
- Run `sbt -Dconfig.resource test.conf` to start the shell with custom _config.resource_ parameter
- Run `;clean;run` - observe failure saying test.conf cannot be found
