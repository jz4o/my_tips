# pydantic custom validation error: Pydantic のValidationErrorを自作する

```py
from pydantic_core import PydanticCustomError, ValidationError

raise ValidationError.from_exception_data(
    '<model name>',
    [
        {
            'type': PydanticCustomError('<error type>', '<error message>'),
            'loc': ('<field name>',),
            'input': '<input value>',
        },
    ],
)
```

## 例

```py
from pydantic import BaseModel, ValidationError
from pydantic_core import PydanticCustomError
from pydantic_core import ValidationError as CoreValidationError


class User(BaseModel):
    id: int
    name: str


# 通常の ValidationError の例
try:
    User(id='bad id', name='user')
except ValidationError as e:
    print(e.__class__)
    # => <class 'pydantic_core._pydantic_core.ValidationError'>

    print(e)
    # =>
    # 1 validation error for User
    # id
    #   Input should be a valid integer, unable to parse string as an integer [type=int_parsing, input_value='bad id', input_type=str]
    #     For further information visit https://errors.pydantic.dev/2.8/v/int_parsing


# 自作した ValidationError の例
try:
    model_name = 'User'
    field_name = 'id'
    input_value = 'bad id'
    error_type = 'int_parsing'
    error_message = 'Input should be a valid integer, unable to parse string as an integer'

    raise CoreValidationError.from_exception_data(
        model_name,
        [
            {
              'type': PydanticCustomError(error_type, error_message),
              'loc': (field_name,),
              'input': input_value,
            },
        ],
    )
except ValidationError as e:
    print(e.__class__)
    # => <class 'pydantic_core._pydantic_core.ValidationError'>

    print(e)
    # =>
    # 1 validation error for User
    # id
    #   Input should be a valid integer, unable to parse string as an integer [type=int_parsing, input_value='bad id', input_type=str]
```

## 補足

* 存在しないモデル名、フィールド名を使用することも可能

    ```py
    from pydantic import ValidationError
    from pydantic_core import PydanticCustomError
    from pydantic_core import ValidationError as CoreValidationError
    
    try:
        model_name = 'NotExistModel'
        field_name = 'not_exist_field'
        input_value = 'bad id'
        error_type = 'int_parsing'
        error_message = 'Input should be a valid integer, unable to parse string as an integer'

        raise CoreValidationError.from_exception_data(
            model_name,
            [
                {
                  'type': PydanticCustomError(error_type, error_message),
                  'loc': (field_name,),
                  'input': input_value,
                },
            ],
        )
    except ValidationError as e:
        print(e.__class__)
        # => <class 'pydantic_core._pydantic_core.ValidationError'>

        print(e)
        # =>
        # 1 validation error for NotExistModel
        # not_exist_field
        #   Input should be a valid integer, unable to parse string as an integer [type=int_parsing, input_value='bad id', input_type=str]
   ```

## 参考

* [pydantic_core.ValidationError.from_exception_data](https://docs.pydantic.dev/latest/api/pydantic_core/#pydantic_core.ValidationError.from_exception_data)
