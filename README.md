Terra Job queue
===============

This symfony app contains the JMS Job Queue Bundle.

It is a proof of concept.

Once the source code is cloned, run:


1. `composer install`
2. Edit `app/config/parameters.yml` to include valid database credentials.
3. `app/console doctrine:database:create`
4. `app/console doctrine:schema:create`
5. `app/console server:run`

Visit http://127.0.0.1:8000/jobs/ and you should see the Jobs overview.

