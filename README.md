## Queue Classic Example

This simple Rails app shows off the features of QueueClassic. Specifically, an application that
users multiple queues with distinct workers. Some files to note:

1. config/initializers/queue_classic.rb
2. db/migrate/20110519195855_add_queue_classic_tables.rb
3. app/models/user.rb
4. app/helpers/users_helper.rb
5. Procfile

### Install

    bundle
    rake db:create
    rake db:migrate
    update DATABASE_URL in config/initializers/queue_classic.rb
    rake qc:load_functions

### Starting Workers

There are 3 queues in this app: Default, email_jobs, image_jobs.

We are only really using email_jobs and image_jobs, so we will attach workers on these queues.

    QUEUE="image_jobs" rake jobs:work
    QUEUE="email_jobs" rake jobs:work

All of this is encoded in our Procfile. You are using Procfile, right?
Now, to start these workers and our web process, execute `foreman start` in the root directory of the app.

### Creating Jobs

    foremant start (If you have not already done so.)

    Visit /users/new
    Click "create"
    Watch output on the worker terminal windows
