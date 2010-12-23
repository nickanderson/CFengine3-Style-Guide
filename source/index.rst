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
All types and classes shoud have a newline between them. Should use the any class explicitly if other classes within a type are used.

Arrows
------
Arrows should be lined up within their scope.

Bundle Curly Brace Alignment
----------------------------
Bundle definition should be followed by a space and a left curly brace, the closing curly brace should be aligned with the first character of the bundle definition. This allows for nested bundles.



Contents:

.. toctree::
   :maxdepth: 2

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


