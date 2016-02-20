
# Response

Although it is important to be able to control the ROV, a large number of tasks
require specialized measuring tools. This protocol is meant to enable these
specialized measurements to be parsed by the top side program for proper
display.

## Logging Responses

The simplest kind of response is one that simply displays to the command line.
These commands will be sorted into different levels of usefullness.

Why use id codes for different message levels? I don't have a good answer for
this question. Why not?

### `log_error` (0x10)

When a serious error occurs and the code cannot continue to run, this will be
sent. I never expect to see this one appear.

```
Payload

    0          4          8
0   +----------+----------+
    |   Message Size (N)  |
1   +                     +
    |                     |
2   +----------+----------+
    |     Character 0     |
... +----------+----------+
    |     Character N     |
N   +----------+----------+
```

### `log_warning` (0x11)

If something unexpected happens, it should be reported with this code.
Officially, it means that an error has occurred, but that the ROV will continue
running.

```
Payload

    0          4          8
0   +----------+----------+
    |   Message Size (N)  |
1   +                     +
    |                     |
2   +----------+----------+
    |     Character 0     |
... +----------+----------+
    |     Character N     |
N   +----------+----------+
```

### `log_info` (0x12)

Pings and confirmation messages should be sent with this code. It means that
everything is running as normal and serves to reassure the pilot about what is
going on.

It's also useful for debugging.

```
Payload

    0          4          8
0   +----------+----------+
    |   Message Size (N)  |
1   +                     +
    |                     |
2   +----------+----------+
    |     Character 0     |
... +----------+----------+
    |     Character N     |
N   +----------+----------+
```

### `log_debug` (0x13)

If something is useful to know for debugging, but would normally just spam the
screen with messages, use this code.

```
Payload

    0          4          8
0   +----------+----------+
    |   Message Size (N)  |
1   +                     +
    |                     |
2   +----------+----------+
    |     Character 0     |
... +----------+----------+
    |     Character N     |
N   +----------+----------+
```