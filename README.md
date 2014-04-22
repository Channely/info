## Information Update
---

### 目录结构

该代码库中必须存在的文件为command.js并且必须保存在一级目录下，在command.js中涉及到的文件必须在该文件中存在。

### 逻辑设计

command.json中记录了本次更新的所有操作，insert 数组中描述了所有的插入数据操作，update数组中描述了所有的数据修改操作，delete中
描述了所有的数据删除操作。

每个操作都需要指定一个该库中存在的json文件,如：

    {
        "new":[
            "project.json","practice.json"
        ],
        "update":[
            "update_a.json","update_b.json"
        ],
        "delete":[
            "delete_practice.json"
        ],
        "cp_file":[
            "cp_file.json"
        ]
    }

该json文件描述了该操作的操作对象特征，或者唯一匹配，或者批量匹配。比如

    //insert information
    "project.json"
    [
        {
            "type":"project",
            "basic": {
                "name": "angular section-one project",
                "desc": "angular section-one project desc",
                "template_tar":"angular part-one template.tar.gz",
                "answer_tar":"AngularJS-LunchMasterDemo.tar.gz",
                "un_tar_name":"angular part-one template"
            }
        },
        {
            "type":"file",
            "basic"{
                "name": "index.html",
                "path": "/angular part-one template/"
            },
            "extra":{
                "extra_file":{
                    //
                }
            }
        },
        {
            "type":"file",
            "basic":{
                "name": "spec.js",
                "path": "/angular part-one template/specs/"
            },
            "extra":[
                {
                    "type":"type",
                    "value":"value",
                }
            ]
        }
    ]

    //update information
    "update_a.json"
    [
        {
            "type":"type",
            "aim":{
                "name":"aim_name"
                //...
            }
            "basic":{
                "column":"value"
                //...
            }
        }
    ]


    //delete information
    "delete_practice.json"
    [
        {
            "type":"aim_type",
            "aim":{
                "name":"aim_name"
                //... specifies
            }
        }
    ]

    //cp a file to template
    cp_file.json
    [
        {
            "source":"AngularJS-LunchMasterDemo.tar.gz",
            "target":"template/AngularJS-LunchMasterDemo.tar.gz"
        }
    ]

### 需要注意

该设计把更新顺序的决策权交到了网站信息的维护者手中，所以，维护者除了要确定要更新什么内容以外还要注意信息更新间的依赖关系，比如：
在新建practice的时候要考虑到该练习所用工程是否存在；在删除信息的时候要考虑到那些信息和该信息仍然存在关联；

由于在JSON中无法动态的获取到存入数据库的实例的ID，在创建关联的时候，一定要注意关联对象之间的唯一确定属性。

信息的维护者应该熟悉需要维护的每一种类型的具体的数据结构。