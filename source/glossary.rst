========
Glossary
========
.. glossary::

    Promiser
        This is the object that formally makes the promise. It is always the
        affected object, since objects can only mkae promises about their own
        state or behaviour in Cfengine. 

    Promisee
        (optional) This is a possible stakeholder, someone who is interested in
        the outcome of the promise. It is used as documentation, and it is used
        for reasoning in the commercial Cfengine product. 

    Promise body
        Everything else about a promise is defined in the body of the promise.
        We use this word in the sense of `body of a contract' or the `body of a
        document' (like <body>) tags in HTML, for example. 

        A promise body is a list of declarations of the following form::

            cfengine_attribute_type => user_defined_value or template

    promise-type
        someting

    class-expression
        see :term:`Classes`

    Classes
        Classes are the double-colon decision syntax in cfengine. They
        determine in what context a promise is made, i.e. when and where.
        Recall the basic syntax of a promise::

            promise-type:
                class-expression::
                    promiser -> promisee
                        attribute => body,
                        ifvarclass => other-class-expression;

        The class expression may contain words like ‘Hr12’, meaning from 12:00
        p.m - 13:00 p.m., or ‘Hr12&Min05_10’, meaning between 12:05 and 12:10.
        Classes may also have spatial descriptors like ‘myhost’ or ‘solaris’,
        which decide which hosts in the namespace, or ‘ipv4_192_168_1_101’
        which decides the location in IPv4 address space.

        If the class expression is true, the promise can be considered made for
        the duration of the current execution.

        Cfengine 3 has a new class predicate ifvarclass which is ANDed with the
        normal class expression, and which is evaluated together with the
        promise. It may contain variables as long as the resulting expansion is
        a legal class expression.
