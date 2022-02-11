# Flask and Celery on Render

This repo can be used as a template for deploying a [Celery](https://github.com/celery/celery) distributed task queue, a [Flower](https://github.com/mher/flower) instance for monitoring Celery through a web front-end, and a simple Flask application on Render using Blueprints - Render's "Infrastructure as code" tooling.


## Usage

1. Use [the template](https://github.com/zachwick/flask_celery_render) to create a new repository which will contain the flask application and the celery task(s).
2. Modify the `repo` lines in `render.yaml` that are labeled "(STEP 2)" with the URL of your newly created repository.
3. Use [the template](https://github.com/zachwick/redis_render) to create a second new repository that contains the files needed to create a redis instance on Render.
4. Modify the `repo` line in `render.yaml` that are labeled "(STEP 4)" to point your redis instance on Render at your newly created repo.
5. Modify the HTTP Basic Auth username and password from `foo` and `bar` respectively to something less easily guessable.
6. Commit your changes to `render.yaml` and push them to the Github repository.
7. Navigate to the [Blueprints](https://dashboard.render.com/blueprints) section of your Render dashboard.
8. Click the "New Blueprint instance" button and select your repo created in Step 1 from the resulting list of repositories.
   1. N.B. If you haven't done so already, you will need to link your Github account with your Render account.
9. Give your new Render Service Group a meaningful name, and allow Render to create the needed instances and environments.
10. Navigate to the newly created redis instance from your [Render Dashboard](https://dashboard.render.com)
11. Copy the "Service Address" and place it as the value of the `CELERY_BROKER_URL` envVar at the bottom of `render.yaml`.
12. Commit this change and push the changes to the Github repository.

At this point, Render should automatically pick up the changed environment variable and then update and redeploy the needed services.

To visit the flask application, navigate to the Service Address of the 'flask' resource created in your Render account.
To visit the flower instance, navigate to the Service Address of the 'flower' resource created in your Render account and use the credentials set in Step 5 above.

