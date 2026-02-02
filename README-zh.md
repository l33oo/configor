<div align="center">

![logo](./assets/logo.png)

<!-- [![Open in VSCode](https://open.vscode.dev/badges/open-in-vscode.svg)](https://open.vscode.dev/l33oo/configor) -->
[![Open in VSCode](https://img.shields.io/badge/open-in%20Visual%20Studio%20Code-blue)](https://open.vscode.dev/l33oo/configor)
[![Github status](https://github.com/l33oo/configor/actions/workflows/unit_tests.yml/badge.svg?branch=master)](https://github.com/l33oo/configor/actions)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/cf98f6b174fe4dd19f1e4574ac527a07)](https://app.codacy.com/gh/l33oo/configor/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)
[![codecov](https://codecov.io/github/l33oo/configor/graph/badge.svg?token=OO71U89I5N)](https://codecov.io/github/l33oo/configor)
[![GitHub release](https://img.shields.io/github/release/l33oo/configor)](https://github.com/l33oo/configor/releases/latest)
[![GitHub license](https://img.shields.io/github/license/l33oo/configor)](https://github.com/l33oo/configor/blob/master/LICENSE)

为 C++11 设计的轻量级配置库

[EN](./README.md) | [中文](./README-zh.md)

</div>

## 特点

- 仅头文件，低接入成本
- STL-like，低学习成本
- 自定义类型转换与序列化
- 完备的 Unicode 支持
- ASCII & 宽字符支持

## 快速上手

创建 JSON 文档对象

```cpp
json::value j;
j["integer"] = 1;
j["float"] = 1.5;
j["string"] = "something";
j["boolean"] = true;
j["user"]["id"] = 10;
j["user"]["name"] = "Leeoo";

json::value j2 = json::object{
    { "null", nullptr },
    { "integer", 1 },
    { "float", 1.3 },
    { "boolean", true },
    { "string", "something" },
    { "array", json::array{ 1, 2 } },
    { "object", json::object{
        { "key", "value" },
        { "key2", "value2" },
    }},
};
```

类型转换 & 序列化:

```cpp
struct User
{
    std::string name;
    int age;

    // 将自定义类型绑定到 configor
    CONFIGOR_BIND(json::value, User, REQUIRED(name), OPTIONAL(age))
};

// User -> json
json::value j = User{"John", 18};
// json -> User
User u = json::object{{"name", "John"}, {"age", 18}};

// User -> string
std::string str = json::dump(User{"John", 18});
// string -> User
User u = json::parse("{\"name\": \"John\", \"age\": 18}");

// User -> stream
std::cout << json::wrap(User{"John", 18});
// stream -> User
User u;
std::cin >> json::wrap(u);
```

更多内容请到 [wiki](https://github.com/l33oo/configor/wiki) 查看。

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=l33oo/configor&type=Date)](https://star-history.com/#l33oo/configor&Date)

## 计划

- [x] 自定义类型转换
- [x] Unicode 支持
- [x] 单元测试覆盖率达到 85%
- [ ] 完善错误信息
- [ ] YAML 支持
- [ ] ini 支持
- [ ] json5 支持
- [ ] SAX 工具
