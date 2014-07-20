---
layout: post
title: When and Why to use Relational Datastreams
---

Pipelines in go are a [powerful idiom](http://blog.golang.org/pipelines).

The [relational data model](http://en.wikipedia.org/wiki/Relational_model) is an extremely effective and succinct way of manipulating large quantities of data.  It is also extremely popular: it puts the **R** in RDBMS and ORM.

Combining the two yields a variety of higher level composable "chunks" that can be used to reliably solve problems.  Depending on how they are constructed, the pipeline stages can be tuned to different performance characteristics.

This approach (and relational algebra) is amenable to two forms of concurrency: pipelining, where results from one query are piped to another as soon as they are available, and parallelism, where many records / tuples are being processed simultaneously.

> Why have parallel database systems become more than a research curiosity?  One explanation is the widespread adoption of the relational data model.  In 1983 relational database systems were just appearing in the marketplace; today they dominate it.  Relational queries are ideally suited to parallel execution; they consist of uniform operations applied to uniform streams of data.  Each operator produces a new relation, so the operators can be composed into highly parallel dataflow graphs.  By streaming the output of one operator into the input of another operator, the two operators can work in series giving pipelined parallelism.  By partitioning the input data among multiple processors and memories, an operator can often be split into many independent operators each working on a part of the data.  This partitioned data and execution gives pipelined parallelism.
>
> -- <cite>DeWitt, David, and Jim Gray. "Parallel database systems: the future of high performance database systems." Communications of the ACM 35.6 (1992): 85-98.</cite>

Go's pipeline constructs match up very well, and can be applied to construct continuous queries which produce new results as soon as new data is available.

In this blog, relational operations are represented as functions which take one or more channels of input tuples or records, and typically return one or more channels which produce output tuples.

That representation brings with it some interesting questions, which correspond to problems in data streams.

> In this model, data does not take the form of persistent relations, but rather arrives in multiple, continuous, rapid, time-varying data streams. ... Examples of such applications include financial applications, network monitoring, security, telecommunications data management, web applications, manufacturing, sensor networks, and others.
>
> --<cite>Babcock, Brian, et al. "Models and issues in data stream systems." Proceedings of the twenty-first ACM SIGMOD-SIGACT-SIGART symposium on Principles of database systems. ACM, 2002.</cite>

You may find that you have already been using these techniques in some of your code; in that case, these articles may provide a broader context.  None of them are intended to be a one size fits all solution.  You'll have to adapt particular implementations of the operations to your needs.  

If you aren't familiar with relational algebra, see [Database in Depth](http://books.google.com/books?id=TR8f5dtnC9IC&lpg=PP1&dq=isbn%3A0596100124&pg=PP1#v=onepage&q&f=false) by C. J. Date for an excellent introduction.  I try to use the same terminology as that book.

Of course, not all problems can be solved in this way, and not all of the ones that can be solved this way should be.  Data stream algorithms are often concerned with how to deal with very large (potentially unending) amounts of data that might be arriving too fast for consumption.  This gives rise to *sub-linear* algorithms, which provide approximate results instead of exact ones.  If you need an exact answer, or don't have to deal with very large data sets, these algorithms may not be appropriate.
