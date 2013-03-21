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
Typically you indent 2 spaces, and never use tabs. Avoid letting the length of a
line exceed 80 characters. Unless there are cases where breaking the line would
break the parsing of the code. (e.g. long commands statements) 

#. Bundle or body definition should be indented 0 times
#. :term`promise-type` should be indented 1 time
#. Promisers should be intented 2 times
#. Promise attributes should be intented 3 times

    ::

        bundle agent update
        {
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
Each :term:`promise-type` should have a newline before the following promise-type.

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
defauted to the special any class. This is conveniant but can cause readability
issues.

    Good::
 
    vars:
        "sudo" slist => { "%operations ALL = ALL" };

      linux::
        "sudo" slist => { "%operations ALL = ALL",
                          "%linuxadmins ALL = ALL" };
 
    files:
        "$(sudoers)" -> { "Operations Team" }
          comment   => "Ensure common admin sudo permissions are granted",
          edit_line => append_if_no_lines("$(sudo)"); 

    Better::

    vars:
      any::
        "sudo" slist => { "%operations ALL = ALL" };
      linux::
        "sudo" slist => { "%operations ALL = ALL",
                          "%linuxadmins ALL = ALL" };
 
    files:
      any::
        "$(sudoers)" -> { "Operations Team" }
          comment   => "Ensure common admin sudo permissions are granted",
          edit_line => append_if_no_lines("$(sudo)"); 


    Ugly::

    vars:
        "sudo" slist => { "%operations ALL = ALL" };

        linux::
            "sudo" slist => { "%operations ALL = ALL",
                              "%linuxadmins ALL = ALL" };

     files:
        any::
            "$(sudoers)" -> "Operations Team"
                comment   => "Ensure common admin sudo permissions are granted",
                edit_line => append_if_no_lines("$(sudo)"); 




Arrows
------
Arrows should be alligned within a :term:`Promise Body` scope.

Bundle Curly Brace Alignment
----------------------------
Bundle definition should be followed by newline, bundle documentation and the
opening curly brace should be aligned at column 0 by it self.

    ::

        bundle agent example(param1)
        # Documentation is helpful
        # param1 - list - a list of items
        {

        }
    
Inline Comments
---------------
Bundles and bodies should include inline documentation. Documentation of
general function and parameters should be done between the bundle and body
definition and the opening curly brace. This allows documetation to be viewed
even while code folding is on, and decreases the likelihood that documentation
is seperated from the bundle or body if copied to a private library.

Promise comments and handle
---------------------------
Comments and handles should be added to each promise. It may be acceptable to
omit this for classes and vars type promises if they are self apparent.
Handles must be unique within a policy. prefixing handles with namespace and
bundlename might be a good idea.


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


