# Client for todo app

## TODO:
- [x] Dynamically get API url (maybe from .env?)
  - Sort of done, now the requests will always be done to the same address with the same protocol on port 8081
- [x] Fix the useless PATCH requests when the *refreshApp* function is called in the ListTodos component
  - Now the page refreshes, new solution may be necessary for a better experience of use
