Validation
[[Python Basic#Type Hint]]
JavaScript validation: [[Zod]]

used by `langchain`, `huggingface`, `fastapi`

Pydantic v2 (v1 -> v2: `@validator` -> `@field_validator`, `.dict()`/`.json()` -> `.model_dump()`/`.model_dump_json()`)

```sh
pip install "pydantic[email]"  # [email] = email-validator, needed by EmailStr
```

``` python
from pydantic import validate_call

@validate_call
def create_user(first_name: str, last_name: str, age: int) -> dict:
	pass
```

v2 coerces where it safely can (`"30"` -> `30`) and raises ValidationError only when it cannot; `strict=True` forbids coercion

``` python
from pydantic import BaseModel

class User(BaseModel):
	name: str
	email: str
	id: int
	
	user_questions: str | None
```

v2: `str | None` is REQUIRED (must be passed, may be None) - write `= None` to make it optional; v1 defaulted these to None

``` python
from pydantic import BaseModel, EmailStr

class User(BaseModel):
    username: str
    email: EmailStr

user1 = {
    "username": "testuser",
    "email": "test@example.com"
}

validUser = User(**user1)
```

Custom validation
``` python
from pydantic import BaseModel, EmailStr, field_validator

class User(BaseModel):
    username: str
    email: EmailStr
    value: int

    # custom       
    # field validator inside the class 
    @field_validator("value")
    @classmethod
    def validate_value(cls, value):
        if value <= 0:
            raise ValueError("value must be positive")
        return value
```


``` python
from typing import List, Optional, Dict, Any

class CompanyAnalysis(BaseModel):
	is_open_source: Optional[bool] = None
	tech_stack: List[str] = []
	...
```