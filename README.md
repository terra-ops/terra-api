Terra API
=========

This is the tool that open up terra commands to the outside world.



Architecture
------------

### Job Queue
JMS Job Queue is a simple and fully integrated into the Symfony console system.

It does exactly the job we need it to.
Works now.

### REST API 
@TODO: Coming Soon.

We have to update the Symfony REST edition.
https://github.com/terra-ops/terra-api/blob/symfony-rest-test/

That distro includes a REST API, a simple web UI, and build in API documentation generation.

We can use some code from my old prototype: https://github.com/jonpugh/aegir4/tree/master/src/Aegir/Provision/Model

It's the same functionality, but with "Apps", "Environments", and "Hosts" as the objects.

The REST API & Web UI will match the CLI as closely as possible.

# Launching

It is a proof of concept.

Once the source code is cloned, run:

1. Get MySQL running. Create a database and a user to connect to it.   
2. `composer install`.
2. Edit `app/config/parameters.yml` to include valid database credentials.
3. `app/console doctrine:database:create`
4. `app/console doctrine:schema:create`
5. `app/console server:run`
  Visit http://127.0.0.1:8000/jobs/ and you should see the Jobs overview.
6. Visit http://127.0.0.1:8000/command to create a "terra status" command. (https://github.com/terra-ops/terra-api/blob/master/src/AppBundle/Controller/DefaultController.php)
7. Go back to http://127.0.0.1:8000/jobs/ and see the "status" command 
8. `app/console jms-job-queue:run` to run the jobs and save the results to the the running database.

