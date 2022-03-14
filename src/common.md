# Common Tips

A few things learned during the years of software development.

## AVOID receive data to be imported as XLS/XLSX

When a user submit a file to processed by a backend, take a list of invoices by example, if this file in the `XLSX`, it will create problems to processed by the application, as:

- Languages don't have native support to parse this type of file
- Third-party libraries thar can parse the file can be very outdated
- It can contains formulas, formatting, references to other files, macros and other useless thing to a data import.
- May have big file sizes, caused by unused things included in the file

All the things listed above can generate some unexpected behavior with the application, a developer will spend a lot time to bypass all the problems, but they will always comeback, because the file format allow them to exist.

**Is preferable** to receive files in CSV/TXT format or other format that contains only raw data, that can be easy parsed and processed by the backend.

## CONSIDER turn off unused machines

When using separated machines (dynos or EC2 instances) to execute other tasks, like background jobs or CRON routines, is a good idea to turn then off and turn on again by demand, when is known that they will be in a idle state for a long time, like weeknights, weekends and holidays.

This can save money at the end of the month and is most cases does not affect how the systems works.

## AVOID shared database between any service

## PREFER to use docker in all backend services

## PREFER use the maximum of the linter

## PREFER use automated validation on CI steps

## PREFER unit tests to integration tests

## CONSIDER validations to all rules

## PREFER security as a routine

## CONSIDER use o technical debt

## AVOID test environment conditionals in app level

## PREFER to use observability patterns

## CONSIDER send emails by a third-party service

## AVOID keep unused code in the codebase

## CONSIDER have a clear/documented architecture and folder structures definitions

## CONSIDER git hooks

## CONSIDER watch important third-party libraries updates

## PREFER state machines
