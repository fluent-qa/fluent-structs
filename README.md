# fluent model 

## get any value or set any value to json or dict like data 

- given different type of data structure:
```python
more_json_dict = """
{
  "characters": {
    "Lonestar": {
      "id": 55923,
      "role": "renegade",
      "items": ["space winnebago", "leather jacket"]
    },
    "Barfolomew": {
      "id": 55924,
      "role": "mawg",
      "items": ["peanut butter jar", "waggy tail"]
    },
    "Dark Helmet": {
      "id": 99999,
      "role": "Good is dumb",
      "items": ["Shwartz", "helmet"]
    },
    "Skroob1": {
      "id": 12345,
      "role": "Spaceballs CEO",
      "items": ["luggage"]
    }
  }
}
"""

more_dict = {
    "characters": {
        "Lonestar": {
            "id": 55923,
            "role": "renegade",
            "items": ["space winnebago", "leather jacket"],
        },
        "Barfolomew": {
            "id": 55924,
            "role": "mawg",
            "items": ["peanut butter jar", "waggy tail"],
        },
        "Dark Helmet": {
            "id": 99999,
            "role": "Good is dumb",
            "items": ["Shwartz", "helmet"],
        },
        "Skroob": {"id": 12345, "role": "Spaceballs CEO", "items": ["luggage"]},
    }
}
```
- get or set value

```python
def test_get_value_by_expression():
    result = fluentmodels.get_value_by_expression(more_dict,"characters.Lonestar")
    assert result == {
            "id": 55923,
            "role": "renegade",
            "items": ["space winnebago", "leather jacket"],
        }
    
def test_set_value_by_express_json():
    result = fluentmodels.set_value_by_expression(more_json_dict,"characters.Lonestar",{})
    result = fluentmodels.get_value_by_expression(result,"characters.Lonestar")
    assert result == {}

```

## Pydantic Model Enhance

- GenericModel: support camelCase and alias field
- YamlGenericModel: support Pydantic to Yaml

## Excel Read and Write Tools

- Read excel data to Pydantic Models
```python
def test_load_objects_from_excel():
    result = read_excel_to_objects("./unit_demo.xlsx", UnitExcelModel)
    print(result)
    print(type(result))



```
- Write to Excel

```python
def test_write_excels():
    u = UnitExcelModel()
    u.unit_name = "质量"
    u.unit_group_name = "kg"
    u1 = UnitExcelModel(unit_name="test1", unit_group_name="group1")
    list_objects = [u, u1]
    exceltools.write_objects_to_excel(list_objects, "unit_demo.xlsx")
    exceltools.write_objects_to_excel(list_objects, "unit_demo.csv")
```
- Read/Write CSV

```python
    write_objects_to_csv("unit.csv",result)
    read_csv_to_objects("unit.csv",UnitExcelModel)
```
## To Do:

- [] DataFrame
- [X] CSV
