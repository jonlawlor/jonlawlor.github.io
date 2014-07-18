---
layout: page
title: About
---

The relational data model is an extremely effective and succinct way of manipulating large quantities of data.  It is also extremely popular: it puts the **R** in RDBMS and ORM.  For an excellent introduction, see [Database in Depth](http://books.google.com/books?id=TR8f5dtnC9IC&lpg=PP1&dq=isbn%3A0596100124&pg=PP1#v=onepage&q&f=false) by C. J. Date.  I try to use the same terminology as that book.

It is also amenable to two forms of concurrency: pipelining, where results from one query are piped to another as soon as they are available, and parallelism, where many records / tuples are being processed simultaneously.  

> Why have parallel database systems become more than a research curiosity?  One explanation is the widespread adoption of the relational data model.  In 1983 relational database systems were just appearing in the marketplace; today they dominate it.  Relational queries are ideally suited to parallel execution; they consist of uniform operations applied to uniform streams of data.  Each operator produces a new relation, so the operators can be composed into highly parallel dataflow graphs.  By streaming the output of one operator into the input of another operator, the two operators can work in series giving pipelined parallelism.  By partitioning the input data among multiple processors and memories, an operator can often be split into many independent operators each working on a part of the data.  This partitioned data and execution gives pipelined parallelism.
>
> -- <cite>DeWitt, David, and Jim Gray. "Parallel database systems: the future of high performance database systems." Communications of the ACM 35.6 (1992): 85-98.</cite>

Go's concurrency constructs match up very well: parallel pipelines are already a [powerful idiom](http://blog.golang.org/pipelines).

In this blog, relational operations are represented as functions which take one or more channels of input tuples or records, and typically return one or more channels which produce output tuples.  That isn't the only way to represent relational algebra, but it does lend itself well to it.

That representation brings with it some interesting questions, which correspond to problems in data streams.

> In this model, data does not take the form of persistent relations, but rather arrives in multiple, continuous, rapid, time-varying data streams. ... Examples of such applications include financial applications, network monitoring, security, telecommunications data management, web applications, manufacturing, sensor networks, and others.
>
> --<cite>Babcock, Brian, et al. "Models and issues in data stream systems." Proceedings of the twenty-first ACM SIGMOD-SIGACT-SIGART symposium on Principles of database systems. ACM, 2002.</cite>

I hope to demonstrate how relations can be represented in idiomatic Go, and that using relational algebra doesn't mean using an SQL server and a query language.  It can be simple and high performance, and can handle the continuous queries that traditional RDBMS solutions can't handle.  I also hope to give a new perspective on existing Go code.

> So Why Go Through All This?
>
> Why take any journey?  Why did the chicken cross the road?  Because in moving from one place to another, we learn something about both.  Maybe you're not the kind of person who needs to know how things work, but if you have your eyeballs on this page, I'm betting you are.  And people like us tinker--that's how we find things out.  For me, following the trail from pizza to brioche just shows the lay of the land.  Seeing how everything is connected rather than just following directions makes me a better cook.
>
> --<cite>Brown, Alton. *I'm Just Here for More Food : Food X Mixing + Heat = Baking.* Toronto: Stewart, Tabori & Chang, 2004. Print.

Have questions or suggestions? Feel free to [email me](mailto:jonathan.lawlor@gmail.com) or [ask me on Twitter](https://twitter.com/jonjlawlor).

Thanks for reading!
