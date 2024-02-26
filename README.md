Build the image dev:

`$ docker-compose build`

Once the image is built, run the container:

`$ docker-compose up -d`

Navigate to http://localhost:8000/ to again view the welcome screen.

> Check for errors in the logs if this doesn't work via docker-compose logs -f.

Bring [down](https://docs.docker.com/compose/reference/down/) the development containers (and the associated volumes with the `-v` flag):

`$ docker-compose down -v`

Then, build the production images and spin up the containers:

`$ docker-compose -f docker-compose.prod.yml up -d --build`

Verify that the `hello_django_prod` database was created along with the default Django tables. Test out the admin page at http://localhost:8000/admin. The static files are not being loaded anymore. This is expected since Debug mode is off. We'll fix this shortly.