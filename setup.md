# Full Stack Setup

## Backend

### Python
- Requirements
  - Python 3
  - pip
  - Node.JS(v6+)
  - npm(5.2+)

1. Create project folder:
  - `$ mkdir project_folder_name`
  - ` cd project_folder_name`

2. Create virtual environment:
  - `python -m venv project_folder_name_venv`
  - `py -m venv project_folder_name_venv`

### Django_REST
- Requirements
  - Django REST Framework

1. Install django rest framework:
  - `pip install djangorestframework`
  - `python3 -m pip install djangorestframework`
  - `py -m pip install djangorestframework`

2. Install app:
- Go to setting.py file and install app:
  ```
  project_name/project_name/setting.py

  INSTALLED_APPS = [
    'rest_framework',
    'corsheaders',
  ]
  ```

### Django
- Requirements
  - Django

1. Install Django:
  - `pip install django`

2. Create Django Backend project:
  - `django-admin startproject project_name`
  
3. Change into backend dir:
  - `cd project_name`

4. Create Django Backend app:
  - `python manage.py startapp django_app_name`
  - `py manage.py startapp django_app_name`

5. Install app:
- Go to setting.py file and install app:
  ```
  project_name/project_name/setting.py

  INSTALLED_APPS = [
    'app',
  ]
  <!-- OR -->

  INSTALLED_APPS = [
    'django_app_name.apps.django_App_name.Config',
  ]
  ```

6. SEE Django_REST

7. Models
- Create model:
  ```
  project_name/django_app_name/models.py


  class Service(models.Model):
    image = models.ImageField(upload_to='uploads/images', null=False, blank=False)
    name = models.CharField(max_length=150, null=False, blank=False)
    price = models.DecimalField(max_digits=7, decimal_places=2, null=False, blank=False)
    description = models.TextField()
    category = models.CharField(max_length=50, null=True, blank=True)

    def __str__(self) -> str:
      return self.name
  ```

- Register model:
  ```
  project_name/django_app_name/apps.py

  # Import model
  from .models import Service

  # Register your models here.
  admin.site.register(Service)
  ```

- Migrate model:
  - `python manage.py makemigrations`
  - `py manage.py makemigrations`
  - `python manage.py migrate`
  - `py manage.py migrate`

- Create superuser:
  - `python manage.py createsuperuser`
  - `py manage.py createsuperuser`
  ```
  Username (leave blank to use 'user'): tester
  Email address: tester@email.com
  Password: 
  Password (again):
  This password is too short. It must contain at least 8 characters.
  This password is too common.
  This password is entirely numeric.
  Bypass password validation and create user anyway? [y/N]:
  ```

8. Serializers:
- Go to django_app_name directory:
  - `cd project_name/django_app_name`
  - `touch serializers.py`
  ```
  project_name/django_app_name/serializers.py

  from rest_framework import serializers 
  from .models import Service

  class ServiceSerializer(serializers.ModelField):
    class Meta:
      model = Service
      # fields = ['image', 'name', 'price', 'description', 'category']
      fields = '__all__'
  ```

9. Views
- Create views:
  ```
  project_name/django_app_name/views.py

  # Import model
  from .models import Service

  # Import serializers
  from .serializers import ServiceSerializer

  # Import viewsets
  from rest_framework import viewsets

  # Create your views here.

  class ServiceView(viewsets.ModelViewSet):
    # Get all services
    queryset = Service.objects.all()
    # Serializer class
    serializer_class = ServiceSerializer
  ```

10. Url's
- Include django_app_name urls:
  ```
  project_name/project_name/urls.py

  # Import Service view
  from django_app_name.views import ServiceView

  # Import route
  from rest_framework import routers

  # Create route instance to handle routing
  route = routers.DefaultRouter()
  route.register('', ServiceView, basename='services')

  urlpatterns = [
    path('admin/', admin.site.urls),
    # Create api path
    path('api/', include(route.urls)),
  ]
  
  # Media redirection using static configurations
  if settings.DEBUG is True:
      urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
  ```

### Database
- Django Admin

1. SEE Django: Models

2. Make migrations for database:
  - `python manage.py makemigrations`
  - `py manage.py makemigrations`

3. Migrate models data to database:
  - `python manage.py migrate`
  - `py manage.py migrate`

4. Create Admin User: 
- See Django: Models - Create superuser

5. Run server:
- `python manage.py runserver`
- `py manage.py runserver`
  ```
  Watching for file changes with StatReloader
  Performing system checks...

  System check identified no issues (0 silenced).
  February 02, 2023 - 08:59:26
  Django version 4.1.3, using settings 'project_name.settings'
  Starting development server at http://127.0.0.1:8000/
  Quit the server with CTRL-BREAK.
  ```

### Media
- Uploading Images

- Pillow
  - `python -m pip install Pillow`
  - `py -m pip install Pillow`

1. In root directory, create media directory to hold uploads/images:
  -  `mkdir media`
  - `cd media`
  - `mkdir uploads`
  - `cd uploads`
  - `mkdir images`

2. Configure media directory:
- Go to setting.py:
  ```
  project_name/project_name/setting.py

  # Static files (CSS, JavaScript, Images)
  # https://docs.djangoproject.com/en/4.1/howto/static-files/

  # Root folder
  MEDIA_ROOT = os.path.join('BASE_DIR', 'media')

  # Redirects uploads to this dir via url
  MEDIA_URL = '/media/'
  ```

3. Configure static redirect:
- Go to urls.py:
  ```
  # Import static
  from django.conf.urls.static import static

  # Import settings
  from django.conf import settings

  urlpatterns = [
      path('admin/', admin.site.urls),
  ]+static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
  # Media redirection using static configurations
  ```




## Frontend

### React
- Requirements
  - Axios
  - React Router DOM
  - React Bootstrap

- Got to Project folder directory:
  - `cd project_folder_name`

1. Create React app:
  - `npx create-react-app react_app_name`

2. Start development server:
  - `cd react_app_name`
  - `npm start`

- Install axios, react-router-dom, react-bootstrap:
  - `npm i axios react-router-dom react-bootstrap bootstrap`

3. Import Bootstrap CSS:
  - Got to index.js or App.js:
    ```
    react_app_name/src/index.js
    react_app_name/src/App.js

    import 'bootstrap/dist/css/bootstrap.min.css';
    ```

4. Components
  - Create components directory:
    - `cd react_app_name/src`
    - `mkdir components`
  
  - Create components file corresponding to each component:
    - Example: Add, Show, Detail, Update, etc..
      - `touch ComponentName.js`

  - ComponentName.js:
    - React Server Component snippet: rsc
      - React Server Components, or “RSC” for short, they are effectively a way to render React apps on the server while keeping component code away from the browser.
      ```
      import React from 'react';

      const ComponentName = () => {
        return (
          <div>
            <h1>Show Data from API</h1>
          </div>
        );
      };

      export default ComponentName;
      ``` 
  
  - Import component:
    -  Go to App.js:
      ```
      // Import Components
      import ComponentName from './components/ComponentName';
      import ComponentName from './components/ComponentName';

      // Import from react-router-dom
      import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';



      function App() {
        return (
          <div className="App">
            <Router>
              <Switch>
                # Home Route
                <Route exact path='/' element={ ComponentName } />
                <Route exact path='/endpoint' element={ ComponentName } />
              </Switch>
            </Router>
          </div>
        );
      }

      export default App;
      ```




5. Routing
  - Import from react-router-dom:
    ```
    react_app_name/src/App.js

    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

    import ComponentName from './components/Component';

    function App() {
      return (
        <div className="App">
          <Router>
            <Navbar />
            <Routes>
              <Route exact path='/' element={ <ComponentName /> } />
              <Route exact path='/addService' element={ <AddComponent /> } />
            </Routes>
          </Router>
        </div>
      );
    }

    export default App;
    ```

  - NavBar:
    ```
    react_app_name/src/components/ComponentName.js

    import { Navbar, Nav } from 'react-bootstrap';
    import { NavLink } from 'react-router-dom';

    const NavbarFunc = () => {
      return (
        <div>
          <Navbar bg="light" expand="lg">
            <Navbar.Brand href="#home">Services</Navbar.Brand>
            <Navbar.Toggle aria-controls="basic-navbar-nav" />
              <Nav className="mr-auto">
                <NavLink className='css-style-selector' to='/'>Services</NavLink>
                <NavLink className='css-style-selector' to='/endpoint'>Nav Link</NavLink>
              </Nav>
          </Navbar>
        </div>
      );
    };

    export default Navbar;
    ```

6. useState(), useEffect(), axios
  - useState(): Set state of application
  - axios: API requests
    ```
    react_app_name/src/components/ComponentName.js

    const ComponentFunction = () => {
      
      # useState() set to empty array
      const [variable, setVariable] = useState([])

      # axios async func
      const getSomething = async () => {

        # await get response
        const response = await axios.get('http://localhost:8000/api/');

        # Set services variable to response data using setVariables func
        setVariable(response.data)

        # useEffect() that runs once on load
        useEffect(() => {
          getSomething();
        }, [])
      }
    }
    ```

7. Card
  - Implement map for card:
    ```
    react_app_name/src/component/ComponentName.js

    // Import Card and Button from Bootstrap
    import { Button, Card } from 'react-bootstrap';

    const ComponentFunc = () => {

      return (
        <div className='services-card-input'>
          {/* Display each service card using map */}
          {
            variable.map((var, index) => (
              <Card className='m-2 rounded shadow-lg' style={{ width: '22rem' }}>
                <Card.Img variant="top" src={ var.image } />
                <Card.Body>
                  <Card.Title>{var.name}</Card.Title>

                  <Card.Text>{var.price}</Card.Text>

                  <Card.Text>{var.description}</Card.Text>

                  <Card.Text>{var.category}</Card.Text>

                  <Button variant="primary">Show Detail</Button>
                </Card.Body>
              </Card>
            ))
          }      
        </div>
      );
    };
    ```


8. Add Component
  - Create add form:
  ```
  react_app_name/src/component/ComponentName.js

  import React, { useState } from 'react';
  import axios from 'axios';
  import { useNavigate } from 'react-router-dom'

  // Set state of add component
  const [file, setFile] = useState(null)
  const [variable, setVariable] = useState('')

  // useNavigate() hooks for redirect..
  const navigate = useNavigate()

  // Add  function
  const addInfoFunc = async () => {
    let formField = new FormData()

    // Append info fields
    formField.append('variable', variable)
    if (file !== null) {
      formField.append('file', file)
    }

    // await form data from API w/ POST request
    await axios({
      method: 'post',
      url: 'http://localhost:8000/api/',
      data: formField
    }).then((response) => {
      console.log(response.data)
      navigate('/')
    })
  }


  return (
    <div>
      <h1>Add Service</h1>

      <div className="container">
        <div className="form-group">

          {/* File Input */}
          <div className="form-group my-2">
            <input
              type="file"
              className="form-control form-control-lg "
              name="image"
              src={image}
              onChange={(e) => setImage(e.target.files[0])}
            />
          </div>

          {/* Variable Input */}
          <div className="form-group my-2">
            <input
              type="text"
              className="form-control form-control-lg "
              placeholder='Enter ...'
              name="variable"
              value={variable}
              onChange={(e) => setName(e.target.value)}
            />
          </div>

          {/* Add button */}
          <button className='btn btn-success' onClick={addServiceInfo}>Add Service</button>
        </div>
      </div>
    </div>
  );
  ```

9. Detail, Update and Delete Component
  - Detail Component
    ```
    react_app_name/src/components/DetailComponent.js

    import axios from 'axios';
    import React, { useState, useEffect} from 'react';
    import { useNavigate, useParams } from 'react-router';
    // import { Card, Button } from 'react-bootstrap';
    import { Link } from 'react-router-dom';

    const DetailComponent = () => {

      // Set state
      const [variable, setVariable] = useState('')

      // useParams() hook for id
      const { id } = useParams();

      // useNavigate for redirect
      const navigate = useNavigate()

      // Get service function by id w/ API GET request
      const getDetail = async () => {
        const { data } = await axios.get(`http://localhost:8000/api/${id}/`)
        console.log(data)
        setVariable(data)
      }

      // useEffect()
      useEffect(() => {
        getDetail()
      }, [])

      - DELETE
      // Delete by id w/ API delete request
      const delete = async (id) => {
        await axios.delete(`http://localhost:800/api/${id}/`)
        navigate('/')
      }

      return (
        <div>
          <h1>Detail</h1>
          
          <div className='single-variable-info'>
            <img src={ variable.image } height='400' width='400' alt="" />
            <p>{ variable.name }</p>
            <p className='variable-price-info'>${ variable.price }</p>
            <p>{ variable.description }</p>
            <p className='variable-category-info'>{ variable.category }</p>

            <Link className='btn btn-success m-2' to={`/${variable.id}/update`} >Update</Link>
            <Link className='btn btn-danger m-2' to={() => delete(variable.id)}>Delete</Link>
          </div>
        </div>
      );
    };
    ```

  - Update Component
    ```
    react_app_name/src/components/UpdateComponent.js

    import React, { useState, useEffect } from 'react';
    import { useNavigate, useParams } from 'react-router-dom';
    import axios from 'axios';

    const UpdateComponentFunc = () => {

      // Set state
      const [file, setFile] = useState(null)
      const [variable, setVariable] = useState('')

      const navigate = useNavigate();
      const { id } = useParams();

      // Load service to update by id w/ API GET request
      const loadUpdate = async () => {
        const { data } = await axios.get(`http://localhost:8000/api/${id}/`);
        console.log(data)

        // Preload data
        setFile(data.file)
        setVariable(data.variable)
      }

      useEffect(() => {
        loadUpdate()
      }, [])

      // Update service info
      const UpdateInfo = async () => {
        let formField = new FormData()

        // Append info
        formField.append('variable', variable)
        ...

        // Check if file input is not empty
        if (file !== null) {
          formField.append('file', file)
        }

        // await form data to update from API w/ PUT request
        await axios({
          method: 'put',
          url: `http://localhost:8000/api/${id}/`,
          data: formField
        }).then((response) => {
          console.log(response.data)
          navigate('/')
        })
      }

      return (
        <div>
          <h1>Update Page</h1>

          <div className="container">
            <div className="form-group">

              {/* Image/File Input */}
              <div className="form-group my-2">
                <img src={file} height='300' width='200' alt="" />
                <input
                  type="file"
                  className="form-control form-control-lg "
                  name="file"
                  src={file}
                  onChange={(e) => setFile(e.target.files[0])}
                />
              </div>

              {/* Variable Input */}
              <div className="form-group my-2">
                <input
                  type="text"
                  className="form-control form-control-lg "
                  placeholder='Enter ...'
                  name="variable"
                  value={variable}
                  onChange={(e) => setVariable(e.target.value)}
                />
              </div>

              {/* Add button */}
              <button className='btn btn-success' onClick={UpdateInfo}>Update</button>
            </div>
          </div>
        </div>
      );
    ```

  - Delete
    - See Detail, Update and Delete Component: Detail Component - DELETE

## Link Backend and Frontend
  - Configure Django to Work w/ ReactJS

1. Install django-cors-headers
  - `pip install django-cors-headers`

2. Install app in django_app_name settings.py
  - See: Backend - Django_REST - Install app

3. Add middleware in django_app_name settings.py
  ```
  MIDDLEWARE = [
      'corsheaders.middleware.CorsMiddleware',
  ]
  ```


## xxx
