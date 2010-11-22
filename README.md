To use:

Pushing jobs:

    $pheanstalk = majaxPheanstalk::getInstance();
    $pheanstalk->useTube('test_tube')->put('Job data');




To run jobs:

Create a worker, modeled after ExampleWorkerThread in lib/thread/, which extends majaxPheanstalkWorkerThread and implements doRun().

    <?php

    class ExampleWorkerThread extends majaxPheanstalkWorkerThread
    {
      protected function doRun()
      {
        $job = $this->getJob('test_tube');
        $data = $job->getData();
        $this->log('Got data: '.$data);
        $this->deleteJob($job);
      }
    }

    ?>


Now you're ready to run the task!


    ./symfony pheanstalk:run_worker ExampleWorkerThread /path/to/store/log/in/

Easy-peasy