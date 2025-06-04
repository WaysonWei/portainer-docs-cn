# 应用模板 JSON 格式

应用模板定义使用 JSON 编写。有效的模板由一个数组组成，每个模板定义包含一个元素。

## 容器模板定义格式

容器模板元素必须是一个有效的 JSON 对象，由必需和可选的数据字段组成。以下是格式示例：

```
{
  "version": "2",
  "templates": [
    {
      // 模板1
    },
    {
      // 模板2
    },
    ...
  ]
}
```

### type

* **描述:** 模板类型
* **格式:** 整数
* **有效值:** `1` = 容器; `2` = Swarm 堆栈; `3` = Compose 堆栈
* **必需/可选:** 必需
* **其他信息:** 类型 `3` 仅限于使用版本 `"2"` 的堆栈格式（这是 docker/libcompose 的限制）

### title

* **描述:** 模板标题
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 必需

### description

* **描述:** 模板描述
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 必需

### image

* **描述:** 与模板关联的 Docker 镜像
* **格式:** 字符串
* **有效值:** 任何有效的 URL
* **必需/可选:** 必需

### administrator-only

* **描述:** 指示模板是否仅对管理员用户可用
* **格式:** 布尔值
* **有效值:** `true` = 仅管理员可用; `false` = 所有用户可用
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "administrator-only": true
}
```

### name

* **描述:** 模板的默认名称（显示在 Portainer UI 中）
* **格式:** 字符串
* **有效值:** 任何有效字符串
* **必需/可选:** 可选

### logo

* **描述:** 模板徽标
* **格式:** 字符串
* **有效值:** 任何有效的 URL
* **必需/可选:** 可选

### registry

* **描述:** 存储 Docker 镜像的注册表。如果未指定，Portainer 将默认使用 Docker Hub
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 可选

### command

* **描述:** 在容器中运行的命令。如果未指定，容器将使用其 Dockerfile 中的默认命令
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "command": "/bin/bash -c \"echo hello\" && exit 777"
}
```

### env

* **描述:** 描述模板所需环境变量的 JSON 数组。数组中的每个元素必须是有效的 JSON 对象。将在模板视图中为数组中的每个元素生成输入。根据对象属性，可以生成不同类型的输入（文本输入、选择）
* **格式:** 数组
* **必需/可选:** 可选

数组格式：

```
{
  "name": "容器镜像支持的环境变量名称（必需）",
  "label": "UI 中输入项的标签（除非存在 set，否则必需）",
  "description": "此输入的简短描述，将在 UI 中作为工具提示显示（可选）",
  "default": "与变量关联的默认值（可选）",
  "preset": "布尔值。如果设置为 true，UI 将不会生成输入（可选）",
  "select": "可能值的数组，将生成选择输入（可选）"
}
```

示例：

```
{
  "env": [
    {
      "name": "MYSQL_ROOT_PASSWORD",
      "label": "Root password",
      "description": "Password used by the root user."
    },
    {
      "name": "ENV_VAR_WITH_DEFAULT_VALUE",
      "default": "default_value",
      "preset": true
    },
    {
      "name": "ENV_VAR_WITH_SELECT_VALUE",
      "label": "An environment variable",
      "description": "A description for this env var",
      "select": [
        {
          "text": "Yes, I agree",
          "value": "Y",
          "default": true
        },
        {
          "text": "No, I disagree",
          "value": "N"
        },
        {
          "text": "Maybe",
          "value": "YN"
        }
      ],
      "description": "Some environment variable."
    }
  ]
}
```

### network

* **描述:** 对应现有 Docker 网络名称的字符串。将在模板视图中自动选择网络
* **格式:** 字符串
* **有效值:** 任何字符串值。如果使用模板时字符串与现有网络名称不匹配，将回退到第一个可用网络
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "network": "host"
}
```

### volumes

* **描述:** 描述与模板关联的卷的 JSON 数组。数组中的每个元素必须是具有必需容器属性的有效 JSON 对象。对于数组中的每个元素，将在启动容器时创建并关联一个 Docker 卷。如果定义了 `bind` 属性，它将用作绑定挂载的源。如果定义了 `readonly` 属性且 = true，卷将以 `readonly` 模式挂载
* **格式:** 数组
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "volumes": [
    {
      "container": "/etc/nginx"
    },
    {
      "container": "/usr/share/nginx/html",
      "bind": "/var/www",
      "readonly": true
    }
  ]
}
```

### ports

* **描述:** 描述模板暴露的端口的 JSON 数组。每个元素必须是有效的 JSON 字符串，指定容器中的端口号以及协议。可以选择性地以端口号和冒号（例如 `8080:`）为前缀来定义要映射到主机上的端口。如果未指定主机端口，Docker 主机将在启动容器时自动分配它
* **格式:** 数组
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "ports": ["8080:80/tcp", "443/tcp"]
}
```

### labels

* **描述:** 描述与模板关联的标签的 JSON 数组。每个元素必须是具有两个属性（`name:` 和 `"<value>"`）的有效 JSON 对象
* **格式:** 数组
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "labels": [
    { "name": "com.example.vendor", "value": "Acme" },
    { "name": "com.example.license", "value": "GPL" },
    { "name": "com.example.version", "value": "1.0" }
  ]
}
```

### privileged

* **描述:** 指示容器是否应以 `privileged` 模式启动。如果未指定，默认为 `false`
* **格式:** 布尔值
* **有效值:** `true` = 以特权模式启动容器; `false` = 不以特权模式启动容器
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "privileged": true
}
```

### interactive

* **描述:** 指示容器是否应以 `foreground` 模式启动。如果未指定，默认为 `false`
* **格式:** 布尔值
* **有效值:** `true` = 以前台模式启动容器; `false` = 不以前台模式启动容器
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "interactive": true
}
```

### restart_policy

* **描述:** 与容器关联的重启策略。如果未指定值，将默认为 `"always"`
* **格式:** 字符串
* **有效值:**
  * `"always"` 无论退出状态如何，始终重启容器
  * `"no"` 从不自动重启容器
  * `"on-failure"` 仅当容器以非零状态退出时才重启容器
  * `"unless-stopped"` 无论退出状态如何，始终重启容器（除非容器被手动停止）
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "restart_policy": "unless-stopped"
}
```

### hostname

* **描述:** 容器的主机名。如果未指定，将默认为 Docker
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "hostname": "mycontainername"
}
```

### note

* **描述:** 关于模板的额外信息，例如其用途。在 Portainer UI 的模板创建表单中显示。支持 HTML
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "note": "You can use this field to record extra information about a template."
}
```

### platform

* **描述:** 支持的平台。在 Portainer UI 中显示一个小的平台相关图标。必须包含有效值
* **格式:** 字符串
* **有效值:** `"linux"`; `"windows"`
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "platform": "linux"
}
```

### categories

* **描述:** 与模板关联的类别数组。填充 Portainer UI 中的类别过滤器
* **格式:** 数组
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "categories": ["webserver", "open-source"]
}
```

## 堆栈模板定义格式

堆栈模板元素必须是一个有效的 JSON 对象，由必需和可选的数据字段组成。以下是格式示例：

```
{
  "type": 2,
  "title": "CockroachDB",
  "description": "CockroachDB cluster",
  "note": "Deploys an insecure CockroachDB cluster, please refer to CockroachDB documentation for production deployments.",
  "categories": ["database"],
  "platform": "linux",
  "logo": "https://cloudinovasi.id/assets/img/logos/cockroachdb.png",
  "repository": {
    "url": "https://github.com/portainer/templates",
    "stackfile": "stacks/cockroachdb/docker-stack.yml"
  }
}
```

### type

* **描述:** 模板类型。Swarm 堆栈将使用等效于 `docker stack deploy` 的方式部署。Compose 堆栈将使用等效于 `docker-compose` 的方式部署
* **格式:** 整数
* **有效值:** `1` = 容器; `2` = Swarm 堆栈; `3` = Compose 堆栈
* **必需/可选:** 必需
* **其他信息:** 类型 `3` 仅限于使用版本 `"2"` 的堆栈格式（这是 docker/libcompose 的限制）

### title

* **描述:** 模板标题
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 必需

### description

* **描述:** 模板描述
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 必需

### repository

* **描述:** 描述从中加载堆栈模板的公共 Git 存储库的 JSON 对象。它指示 Git 存储库的 URL 以及存储库中 Compose 文件的路径
* **格式:** 对象
* **有效值:** 见下面的示例
* **必需/可选:** 必需

此值**必须**引用一个 Git 存储库

对象格式：

```
{
  "url": "公共 git 存储库的 URL（必需）",
  "stackfile": "存储库中 Compose 文件的路径（必需）",
}
```

示例：

```
{
  "url": "https://github.com/portainer/templates",
  "stackfile": "stacks/cockroachdb/docker-stack.yml"
}
```

### administrator_only

* **描述:** 指示模板是否仅对管理员用户可用
* **格式:** 布尔值
* **有效值:** `true` = 仅管理员可用; `false` = 所有用户可用
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "administrator_only": true
}
```

### name

* **描述:** 模板的默认名称（显示在 Portainer UI 中）
* **格式:** 字符串
* **有效值:** 任何有效字符串
* **必需/可选:** 可选

### logo

* **描述:** 模板徽标
* **格式:** 字符串
* **有效值:** 任何有效的 URL
* **必需/可选:** 可选

### env

* **描述:** 描述模板所需环境变量的 JSON 数组。数组中的每个元素必须是有效的 JSON 对象。将在模板视图中为数组中的每个元素生成输入。根据对象属性，可以生成不同类型的输入（文本输入、选择）
* **格式:** 数组
* **必需/可选:** 可选

将在模板视图中为数组中的每个元素生成输入。根据对象属性，可以生成不同类型的输入（文本输入、选择）

数组格式：

```
{
  "name": "容器镜像支持的环境变量名称（必需）",
  "label": "UI 中输入项的标签（除非存在 set，否则必需）",
  "description": "此输入的简短描述，将在 UI 中作为工具提示显示（可选）",
  "default": "与变量关联的默认值（可选）",
  "preset": "布尔值。如果设置为 true，UI 将不会生成输入（可选）",
  "select": "可能值的数组，将生成选择输入（可选）"
}
```

示例：

```
{
  "env": [
    {
      "name": "MYSQL_ROOT_PASSWORD",
      "label": "Root password",
      "description": "Password used by the root user."
    },
    {
      "name": "ENV_VAR_WITH_DEFAULT_VALUE",
      "default": "default_value",
      "preset": true
    },
    {
      "name": "ENV_VAR_WITH_SELECT_VALUE",
      "label": "An environment variable",
      "description": "A description for this env var",
      "select": [
        {
          "text": "Yes, I agree",
          "value": "Y",
          "default": true
        },
        {
          "text": "No, I disagree",
          "value": "N"
        },
        {
          "text": "Maybe",
          "value": "YN"
        }
      ],
      "description": "Some environment variable."
    }
  ]
}
```

### note

* **描述:** 关于模板的额外信息，例如其用途。在 Portainer UI 的模板创建表单中显示。支持 HTML
* **格式:** 字符串
* **有效值:** 任何字符串值
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "note": "You can use this field to record extra information about a template."
}
```

### platform

* **描述:** 支持的平台。在 Portainer UI 中显示一个小的平台相关图标。必须包含有效值
* **格式:** 字符串
* **有效值:** `"linux"`; `"windows"`
* **必需/可选:** 可选
* **示例:** 见下文

```
{ "platform": "linux" }
```

### categories

* **描述:** 与模板关联的类别数组。填充 Portainer UI 中的类别过滤器
* **格式:** 数组
* **必需/可选:** 可选
* **示例:** 见下文

```
{
  "categories": ["webserver", "open-source"]
