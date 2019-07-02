---
key: 20190702
title: "[Module] json 데이터에서 특정 키와 값을 삭제하는 모듈"
categories: programming
comments: true
tag : [python, programming, module]
---



## Module

코드: https://github.com/lifeisgouda/my_python_modules/tree/master/json_key_remover

JSON 데이터에서 특정 key(여기서는 ` coordinates`)에서 값이 `[0, 0]`일 경우 해당 키를 삭제하는 모듈이다.

json의 뎁스가 워낙 깊고, 검사해야할 부분이 많아서 부득이하게 3중 for문이 사용되었다. 

```python
class JSON_KEY_REMOVER:
    def __init__(self):
        self.data = []

    def import_json(self, filename):
        import json

        with open(filename) as json_file:
            self.data = json.load(json_file)

        print('import json done')

    def del_daily_zero_coordinates(self):
        import json

        for k in range(len(self.data)):
            for i in range(len(self.data[k]["history"]["dateInformation"][2]["daily"])):
                for j in range(0, 24):
                    if [0, 0] == self.data[k]["history"]["dateInformation"][2]["daily"][i]["dailyTimeline"]['dateT'+str(j)]["coordinates"]:
                        del self.data[k]["history"]["dateInformation"][2]["daily"][i]["dailyTimeline"]['dateT'+str(j)]["coordinates"]

        with open('data.json', 'w', encoding='UTF-8-sig') as data_file:
            self.data = json.dump(self.data, data_file, ensure_ascii=False)

        print("Done!")
```



## 사용

```python
# main.py

import json_key_remover

remove = json_key_remover.JSON_KEY_REMOVER
remove.import_json("./user.json")
remove.del_daily_zero_coordinates()
```

