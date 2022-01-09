## microURLs: Benchmarks

- Likely the elixir community will be working on these things? QUALITY BEFORE SPEED OR OUCH! 

- Supply : Demand

  - Sysbench is what I usually use to evaluate hardware resource availability (SUPPLY).
  - Dedicated hardware makes that easier than local VMs or cloud VMs.
  - Strain a small system by running (several small or a large) gzip file being written or read from disk.  See how that affects supply demand dynamics.

  - Usually we want to know the read:write (GET:POST) ratio of a given site. (Software demand)
  - Benchmarking databases is COMPLETELY different from benchmarking web apps.  Usually we work to split reads and writes.  We test databases last.

- Benchmarks
  - We would also want to verify from another benchmarking tool?
  - We also want to find elixir tools that are equivalent to the Rail7 benchmark utility:   
    - https://blog.saeloun.com/2021/02/25/rails-allows-benchmark-method-to-be-called-from-anywhere.html

  - My guess is that benchee is a nice tool for testing elixir apps.
    - https://www.toptechskills.com/elixir-phoenix-tutorials-courses/benchmark-elixir-code-benchee/

  - Six big stats are worth looking at:
    - GET singletons in parallel
    - POST singletons in parallel
    - GET in batch (assumes parallelized and need rule: [ reject bad rows | reject entire job ] )
    - POST in batch
    - POST + GET (vanilla OR use last insertID OR cache POST result) => Mix insert and update POSTs
    - % js code

  - Testing use of elixir mnesia cache vs redis cache would be interesting too:  https://www.cloudbees.com/blog/elixir-ets-vs-redis

  - With each web app request round trip, we will also want to see timelines:
    - latency from client request
    - cache hit or database call
    - response first byte
    - response last byte
    - latency in server response

  - Another interesting option for identifying bottlenecks...  Use 2+GB RAM disk as ephemeral DBMS data store where DISK IO is absent.  This way we are testing the database processes BUT not testing disk IO.

- Testing Scale
  - All of the above does not regard scalability:  Just setting supply/demand benchmarks.  Choosing  apps to benchmark comes last.

  - When we scale, we assume all of the work above is done, and then we ask:
    - When we ask this system to do twice as much, does it take twice as long, or longer?
    - "Twice as much" could include size of task per user OR task count per task type per user OR number of users OR etc

- QUALITY BEFORE SPEED OR OUCH! :)
