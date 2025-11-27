Validation
[[Python Basic#Type Hint]]
JavaScript validation: [[Zod]]

used by `langchain`, `huggingface`, `fastapi`

```sh
pip install pydantic
```

``` python
from pydantic import validate_call

@validate_call
def create_user(first_name: str, last_name: str, age: int) -> dict:
	pass
```

Pydantic will check and raise error is type is mismatched 

``` python
from pydantic import BaseModel

class User(BaseModel):
	name: str
	email: str
	id: int
	
	user_questions: str | None
```

``` python
from pydantic import BaseModel, EmailStr

class User(BaseModel):
    username: str
    password: EmailStr

user1 = {
    "username": "testuser",
    "password": "test@example.com"
}

validUser = User(**user1)
```

Custom validation
``` python
class User(BaseModel):
    username: str
    password: EmailStr
    value: int

    # custom       
    # field validator inside the class 
    @field_validator("value")
    def validate_value(cls, value):
        if value <= 0:
            raise ValueError(f"account_id must be positive")
        return value
```


``` python
from typing import List, Optional, Dict, Any

class CompanyAnalysis(BaseModel):
	is_open_source: Optional[bool] = None
	tech_stack: List[str] = []
	...
```