workload-ref-archs Style Commandments
=====================================

- Read the OpenStack Style Commandments
  http://docs.openstack.org/developer/hacking/

- Read the `OpenStack Documentation Contributor Guide`_,
  especially the `Writing style`_, `RST conventions`_
  and `Diagram guidelines`_

.. _OpenStack Documentation Contributor Guide: http://docs.openstack.org/contributor-guide
.. _Writing style: http://docs.openstack.org/contributor-guide/writing-style.html
.. _RST conventions: http://docs.openstack.org/contributor-guide/rst-conv.html
.. _Diagram guidelines: http://docs.openstack.org/contributor-guide/diagram-guidelines.html

Proposing a new Workload Reference Architecture
-----------------------------------------------

- Anyone can propose new Workload Reference Architecture
- Anyone can propose to enhance or modify existing Workload Reference
  Architecture
- All proposal will be reviewed by the core team members of Enterprise WG

Submission Process
------------------

#. Follow the instructions at `First timers <http://docs.openstack.org/contributor-guide/quickstart/first-timers.html>`_
   to configure a local environment.

#. Clone the repository::

    git clone https://github.com/openstack/workload-ref-archs.git

#. Create a branch for the new workload ::

    git checkout -b <workload-name>

#. Create the following directory structures under `workload-ref-archs <workload-ref-archs>`_
   for the new workload::

    <workload-name>
    <workload-name>/<workload-name>.rst
    <workload-name>/figure
    <workload-name>/sample/heat
    <workload-name>/sample/murano

   .. list-table::
      :widths: 15 25

      * - <workload-name>.rst 
        - Provides a full description of the workload.
          Please follow the structure in `workload-template.rst <workload-ref-archs/workload-template.rst>`_

      * - figure
        - Include all images in this folder

      * - sample/heat
        - Include sample code for heat (if any)

      * - sample/murano
        - Include sample code for murano (if any)

#. Commit the changes::

    git commit -a -m "new workload <workload-name>"

#. Submit the changes for review, use the "new-workload" topic for new
   workload::

    git review -t new-workload

#. The core reviewers of the Workload Reference Architectures team will review
   the submision.

