# Pino Sentry transport

![NPM](https://img.shields.io/npm/l/pino-nextjs-sentry-transport)
[![npm version](https://img.shields.io/npm/v/pino-nextjs-sentry-transport)](https://www.npmjs.com/package/pino-nextjs-sentry-transport)
[![GitHub Workflow Status](https://github.com/dfr-exnaton/pino-nextjs-sentry-transport/actions/workflows/pino-nextjs-sentry-transport.yml/badge.svg?branch=main)](https://github.com/dfr-exnaton/pino-nextjs-sentry-transport/actions)

This module provides a 'transport' for pino that sends errors to Sentry.

## Install

```shell
npm i @sentry/node pino-nextjs-sentry-transport
```

## usage

```typescript
import pino from "pino";

const logger = pino({
  transport: {
    target: "pino-nextjs-sentry-transport",
    options: {
      sentry: {
        dsn: "https://<key>:<secret>@sentry.io/<project>",
        // additional options for sentry
      },
      withLogRecord: true, // default false - send the log record to sentry as a context.(if its more then 8Kb Sentry will throw an error)
      tags: ["id"], // sentry tags to add to the event, uses lodash.get to get the value from the log record
      context: ["hostname"], // sentry context to add to the event, uses lodash.get to get the value from the log record,
      minLevel: 40, // which level to send to sentry
      skipSentryInitialization: true, // default false - if you want to initialize sentry by yourself
    },
  },
});
```

if log contain error, it will send to sentry using captureException if not it will use captureMessage.
