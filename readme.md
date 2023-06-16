# Timestamp

This library is a date & time library based on the C `time.h`.\
Keep in mind that this library links with LibC!

## Installation

Clone this repository in your libs folder.

```sh
git clone https://github.com/Nightyx-remy/timestamp
```

Then add the following line in the `build.zig`:

```zig
const timestamp = @import("libs/timestamp/build.zig");

pub fn build(b: *Build) !void {
    ...
    exe.addModule("timestamp", timestamp.module(b));
    try timestamp.link(b, exe);
}
```

## Usage

```zig
const std = @import("std");
const timestamp = @import("timestamp");
const Timestamp = timestamp.Timestamp;

pub fn main() {
    // Get the current UTC time & date
    const utc_now = Timestamp.now_utc();
    std.debug.print("{}/{}/{} {}:{}:{}\n", .{
        utc_now.date.month_day,
        @enumToInt(utc_now.date.month),
        utc_now.date.year,

        utc_now.time.hour,
        utc_now.time.minute,
        utc_now.time.second
    });

    // Get the current local time & date
    const local_now = Timestamp.now_local();
    std.debug.print("{}/{}/{} {}:{}:{}\n", .{
        local_now.date.month_day,
        @enumToInt(local_now.date.month),
        local_now.date.year,

        local_now.time.hour,
        local_now.time.minute,
        local_now.time.second
    });
}
```
