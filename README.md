## Project Setup Instructions

### Development Environment Setup

1. **Build the Development Image:**

   Begin by building your development Docker image with the following command:

   ```bash
   docker-compose build
   ```

2. **Run the Development Container:**

   Once the image is successfully built, start your development container in detached mode:

   ```bash
   docker-compose up -d
   ```

3. **Accessing the Application:**

   With the container running, access the application by navigating to [http://localhost:8000/](http://localhost:8000/) in your web browser. You should see the welcome screen.

   If the application doesn't load, check for potential errors in the container logs:

   ```bash
   docker-compose logs -f
   ```

4. **Shutting Down Development Environment:**

   To stop and remove the development containers and associated volumes, use the following command:

   ```bash
   docker-compose down -v
   ```

### Production Environment Setup

1. **Building and Running Production Containers:**

   For the production environment, build and start the containers with:

   ```bash
   docker-compose -f docker-compose.prod.yml up -d --build
   ```

2. **Database and Django Setup:**

   After the containers are up, ensure the `hello_django_prod` database is created along with the default Django tables by running migrations:

   ```bash
   docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
   ```

   Then, collect static files:

   ```bash
   docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
   ```

3. **Verifying Static Files:**

   Requests to static files (e.g., `http://localhost:1337/static/*`) should now be served from the "staticfiles" directory. Verify this by accessing [http://localhost:1337/admin](http://localhost:1337/admin). The static assets should load correctly, indicating that everything is set up properly.

4. **Logging and Troubleshooting:**

   If you encounter issues, consult the logs for more detailed information:

   ```bash
   docker-compose -f docker-compose.prod.yml logs -f
   ```

5. **Shutting Down Production Environment:**

   To stop the production containers and remove associated volumes, use the same command as for the development environment:

   ```bash
   docker-compose down -v
   ```

### Notes

- Ensure Docker and Docker Compose are installed on your system before beginning the setup process.
- Adjust the `docker-compose.yml` and `docker-compose.prod.yml` files as necessary to fit your project's requirements.
- For detailed Docker and Docker Compose documentation, visit [Docker Docs](https://docs.docker.com/).