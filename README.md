# callgrind-splitter

Usage: `./callgrind-splitter <input-file> <output-prefix>`

This script will split a series of concatenated callgrind files back into the
original callgrind files.

It is especially useful when extracting profiling information obtained using the
scalyr agent's profiling feature because the agent will upload each run of the
profiler under the same logfile name `agent.callgrind`.

This means that if you use something like the
[scalyr-tool](https://github.com/scalyr/scalyr-tool) to download the profiling
information, it is likely that the downloaded file will contain multiple
callgrind files that were each output during the time interval of interest.

For example, say a customer has turned on profiling for their agents, and we
want to obtain the profiles from a specific serverHost.  You would run the
scalyr tool with the following options to get the profiling data from that
serverHost over the previous 24h:

   ./scalyr download-log --serverHost <server-host> --logfile agent.callgrind --start 24h > agent.callgrind

Then you could use `callgrind-splitter` to split that out in to multiple files,
each prefixed with `agent-`:

   ./callgrind-splitter agent.callgrind agent-

If the original `agent.callgrind` file contained 4 different profiling runs the
output will be split into `agent-01.callgrind`, `agent-02.callgrind`,
`agent-03.callgrind` and `agent-04.callgrind`.

Each of these can then be loaded in a program that allows you to view callgrind
files.

