Install Message Que
===================

A Message Que is optional
-------------------------

Installing a message que system is completely optional. If you don't install one, the tasks run from cron as configured in your standard install will do the same work eventually anyway. 

Installing a message que simply means that in certain important places, work will happen instantly instead of after a delay.

For example, when a user adds a new import the import will be processed and the user can see the results straight away. If you don't have a message que it will happen after a delay.

Supported Message Que Software - Beanstalkd
-------------------------------------------

To use Beanstalkd, simply configure the options:

.. code-block:: php

    $CONFIG->useBeanstalkd = true;
    $CONFIG->beanstalkdHost = 'localhost';
    $CONFIG->beanstalkdPort = 11300;
    $CONFIG->beanstalkdTube = 'openacalendar';

Running a Message Que consumer
------------------------------

Simply run

    php core/cli/runMessageQueConsumer.php

Note each worker will die after a certain amount of time, as configured by 'messageQueConsumerProcessRunsForSeconds'. You should regularly start a new one using cron to replace the one that has died.

This is simply a way to control memory usage in long running processes, by making sure the process stops and starts again with a clean footprint regularly.

Upgrading OpenACalendar when running a Message Que
--------------------------------------------------

Before upgrading, stop any existing running message que consumers.

Make sure to restart some new ones after upgrading.

