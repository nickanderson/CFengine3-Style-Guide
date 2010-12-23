.. CFengine3 Style Guide documentation master file, created by
   sphinx-quickstart on Wed Dec 22 18:28:01 2010.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

==============================
CFengine3 Style Guide Proposal
==============================
Based on Christian Pearces notes
http://www.pearcec.com/cfengine_styleguide.html

Whitespace
==========
Indentation and Line Length
---------------------------
Typically you indent 4 spaces, and never use tabs. Never let the length of a
line exceed 80 characters. Unless there are cases where breaking the line would
break the parsing of the code. (i.e. long shellcommands statements) 

    ::

        bundle agent update {
            vars:
                "policyhost" string => "MyPolicyServerHostname";

            files:
                any::
                    "/var/cfengine/inputs/"
                        copy_from    => update_policy( "/var/cfengine/masterfiles","$(policyhost)" ),
                        classes      => policy_updated( "policy_updated" ),
                        depth_search => recurse("inf");

                solaris::
                    "/var/cfengine/inputs"
                        copy_from => update_policy( "/var/cfengine/masterfiles", "$(policyhost" ),
                        classes   => policy_updated( "policy_updated" );
        }

Types and classes within bundles
--------------------------------
Each :term:`promise-type` should have newline before the following promise-type.

    For example the newline before the files promise-type::

        vars:
            "policyhost" string => "MyPolicyServerHostname";

        files:
            any::
                "/var/cfengine/inputs/"
                    copy_from    => update_policy( "/var/cfengine/masterfiles","$(policyhost)" ),
                    classes      => policy_updated( "policy_updated" ),
                    depth_search => recurse("inf");


Each :term:`class-expression` within a promise-type should have a newline before the 
following class-expression.

    ::
        
        files:
           any::
               "/var/cfengine/inputs/"
                   copy_from    => update_policy( "/var/cfengine/masterfiles","$(policyhost)" ),
                   classes      => policy_updated( "policy_updated" ),
                   depth_search => recurse("inf");

           solaris::
               "/var/cfengine/inputs"
                   copy_from => update_policy( "/var/cfengine/masterfiles", "$(policyhost" ),
                   classes   => policy_updated( "policy_updated" );

The any class-expression
~~~~~~~~~~~~~~~~~~~~~~~~
The any class-expression is special in that it is not syntatically required 
within a promise-type. Promisers defined directly under a promise-type are
defauted to the special any class. This is conveniant but causes readability
issues.

To improve readability by aligning all class-expressions within a type, the
special any class-expression should be explicitly defined when additional
class-expressions are used. If no class-expression other than the special 
any class is used it is not necissary to explicitly state it.

Arrows
------
Arrows should be alligned within a :term:`Promise Body` scope.

Bundle Curly Brace Alignment
----------------------------
Bundle definition should be followed by a space and a left curly brace, the closing curly brace should be aligned with the first character of the bundle definition. This allows for nested bundles.

    ::
        bundle agent example {

        }
    


Contents:

.. toctree::
   :maxdepth: 2
   :glob:

   glossary
   */*

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


