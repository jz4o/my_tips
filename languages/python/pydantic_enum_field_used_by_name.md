# pydantic enum field used by name: Pydantic の Enum のフィールドを名前で扱う

```py
from enum import StrEnum

from pydantic import BaseModel, Field, field_validator
from pydantic_core import PydanticCustomError


class EnumField(StrEnum):
    FIELD_1_KEY = 'FIELD_1_VALUE'
    FIELD_2_KEY = 'FIELD_2_VALUE'
    FIELD_3_KEY = 'FIELD_3_VALUE'

    @classmethod
    def names(cls):
        return [e.name for e in cls]

    @classmethod
    def find_by_name(cls, key_name):
        return next(iter([e for e in cls if e.name == key_name]), None)

class EnumNameModel(BaseModel):
    field: EnumField = Field(...)

    @field_validator('field', mode='before')
    @classmethod
    def convert_field_from_enum_name(cls, field: str) -> EnumField:
        enum_field = EnumField.find_by_name(field)
        if enum_field is None:
            if len(EnumField) == 1:
                message = f"Input should be '{next(iter(EnumField)).name}'"
            else:
                enum_field_names = [f"'{name}'" for name in EnumField.names()]
                values = f'{", ".join(enum_field_names[:-1])} or {enum_field_names[-1]}'

                message = f'Input should be {values}'

            raise PydanticCustomError('enum', message)

        return enum_field

EnumNameModel(field='FIELD_1_KEY')
# => field=<EnumField.FIELD_1_KEY: 'FIELD_1_VALUE'>

EnumNameModel(field='FIELD_2_VALUE')
# => 
# pydantic_core._pydantic_core.ValidationError: 1 validation error for EnumNameModel
# field
#   Input should be 'FIELD_1_KEY', 'FIELD_2_KEY' or 'FIELD_3_KEY' [type=enum, input_value='FIELD_2_VALUE', input_type=str]
```

## 通常の Enum の場合の例

```py
from enum import StrEnum

from pydantic import BaseModel, Field


class EnumField(StrEnum):
    FIELD_1_KEY = 'FIELD_1_VALUE'
    FIELD_2_KEY = 'FIELD_2_VALUE'
    FIELD_3_KEY = 'FIELD_3_VALUE'

class EnumValueModel(BaseModel):
    field: EnumField = Field(...)

EnumValueModel(field='FIELD_1_VALUE')
# => field=<EnumField.FIELD_1_KEY: 'FIELD_1_VALUE'>

EnumValueModel(field='FIELD_2_KEY')
# =>
# pydantic_core._pydantic_core.ValidationError: 1 validation error for EnumValueModel
# field
#   Input should be 'FIELD_1_VALUE', 'FIELD_2_VALUE' or 'FIELD_3_VALUE' [type=enum, input_value='FIELD_2_KEY', input_type=str]
```

## 確認環境

* pydantic: 2.9.2
* pydantic_core: 2.23.4
