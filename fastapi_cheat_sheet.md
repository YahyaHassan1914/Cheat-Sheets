# FastAPI Advanced Cheat Sheet

## 1. **Installation**

- Install FastAPI and Uvicorn (ASGI server):
  ```sh
  pip install fastapi uvicorn
  ```

## 2. **Importing FastAPI**

- Import the FastAPI module and other relevant modules:
  ```python
  from fastapi import FastAPI, Depends, HTTPException, Query, Path, Body, Header, Request
  from pydantic import BaseModel, Field
  from typing import Optional, List, Dict, Any
  from fastapi.responses import JSONResponse
  from fastapi.middleware.cors import CORSMiddleware
  ```

## 3. **Creating an App**

- Create an instance of the FastAPI class:
  ```python
  app = FastAPI()
  ```

## 4. **Creating Routes**

- Define routes using decorators:
  ```python
  @app.get("/path")
  async def get_endpoint():
      return {"message": "GET request successful"}

  @app.post("/path")
  async def post_endpoint(data: dict):
      return {"received_data": data}
  ```

## 5. **Path Parameters**

- Access path parameters:
  ```python
  @app.get("/items/{item_id}")
  async def get_item(item_id: int):
      return {"item_id": item_id}
  ```

## 6. **Query Parameters**

- Define query parameters:
  ```python
  @app.get("/items")
  async def get_items(skip: int = Query(0, description="Number of items to skip"), limit: int = Query(10, le=100)):
      return {"skip": skip, "limit": limit}
  ```

## 7. **Request Body**

- Define request body models using Pydantic:
  ```python
  class Item(BaseModel):
      name: str
      price: float
      description: Optional[str] = None
      tax: Optional[float] = None

  @app.post("/items")
  async def create_item(item: Item):
      return {"item": item}
  ```

## 8. **Response Models**

- Define response models:
  ```python
  @app.get("/items/{item_id}", response_model=Item)
  async def get_item(item_id: int):
      return {"name": "Item Name", "price": 9.99}
  ```

## 9. **Path Operations with Multiple Methods**

- Use different HTTP methods for the same path:
  ```python
  @app.get("/items/{item_id}")
  async def read_item(item_id: int):
      return {"item_id": item_id}

  @app.put("/items/{item_id}")
  async def update_item(item_id: int, item: Item):
      return {"item_id": item_id, "updated_item": item}
  ```

## 10. **Middleware**

- Use middleware to process requests and responses:
  ```python
  @app.middleware("http")
  async def add_process_time_header(request: Request, call_next):
      import time
      start_time = time.time()
      response = await call_next(request)
      process_time = time.time() - start_time
      response.headers["X-Process-Time"] = str(process_time)
      return response
  ```

## 11. **Exception Handling**

- Handle exceptions globally:
  ```python
  @app.exception_handler(HTTPException)
  async def http_exception_handler(request: Request, exc: HTTPException):
      return JSONResponse(
          status_code=exc.status_code,
          content={"detail": exc.detail},
      )

  @app.exception_handler(Exception)
  async def generic_exception_handler(request: Request, exc: Exception):
      return JSONResponse(
          status_code=500,
          content={"detail": "An unexpected error occurred."},
      )
  ```

## 12. **Dependency Injection**

- Use dependencies to manage common logic:
  ```python
  async def common_parameters(q: Optional[str] = Query(None, min_length=3, max_length=50)):
      return {"q": q}

  @app.get("/items/")
  async def read_items(commons: dict = Depends(common_parameters)):
      return commons
  ```

## 13. **Security**

- Basic authentication:
  ```python
  from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm

  oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

  @app.post("/token")
  async def login(form_data: OAuth2PasswordRequestForm = Depends()):
      return {"access_token": form_data.username, "token_type": "bearer"}
  ```

- Dependency with OAuth2PasswordBearer:
  ```python
  async def get_current_user(token: str = Depends(oauth2_scheme)):
      return {"token": token}
  ```

## 14. **CORS (Cross-Origin Resource Sharing)**

- Configure CORS middleware:
  ```python
  app.add_middleware(
      CORSMiddleware,
      allow_origins=["*"],  # List of origins
      allow_credentials=True,
      allow_methods=["*"],  # List of methods
      allow_headers=["*"],  # List of headers
  )
  ```

## 15. **File Uploads**

- Handle file uploads:
  ```python
  from fastapi import File, UploadFile

  @app.post("/uploadfile/")
  async def upload_file(file: UploadFile = File(...)):
      return {"filename": file.filename}
  ```

## 16. **Background Tasks**

- Run background tasks:
  ```python
  from fastapi import BackgroundTasks

  def write_log(message: str):
      with open("log.txt", mode="a") as log:
          log.write(message + "\n")

  @app.post("/send/")
  async def send_email(email: str, background_tasks: BackgroundTasks):
      background_tasks.add_task(write_log, f"Sent email to {email}")
      return {"message": "Email sent"}
  ```

## 17. **WebSocket Support**

- Create a WebSocket endpoint:
  ```python
  from fastapi import WebSocket

  @app.websocket("/ws/{client_id}")
  async def websocket_endpoint(websocket: WebSocket, client_id: int):
      await websocket.accept()
      await websocket.send_text(f"Hello client {client_id}")
      while True:
          data = await websocket.receive_text()
          await websocket.send_text(f"Message text was: {data}")
  ```

## 18. **Testing**

- Use `pytest` and `httpx` for testing:
  ```python
  from fastapi.testclient import TestClient
  from myapp import app

  client = TestClient(app)

  def test_read_main():
      response = client.get("/")
      assert response.status_code == 200
      assert response.json() == {"message": "Hello, FastAPI!"}
  ```

## 19. **Performance Tips**

- **Use `async` and `await`**: Utilize asynchronous operations to handle I/O-bound tasks.
- **Limit Logging**: Avoid excessive logging in production to reduce I/O operations.
- **Optimize Queries**: Use efficient database queries and indexing.

## 20. **Deployment**

- **Deploy with Docker**: Create a Dockerfile to containerize the application.
- **Use Uvicorn with Gunicorn**: For production deployment, use Gunicorn with Uvicorn workers:
  ```sh
  gunicorn -w 4 -k uvicorn.workers.UvicornWorker myapp:app
  ```

This advanced cheat sheet covers a broad range of FastAPI features and best practices to help you build efficient and scalable APIs. For more detailed information, refer to the [official FastAPI documentation](https://fastapi.tiangolo.com/).