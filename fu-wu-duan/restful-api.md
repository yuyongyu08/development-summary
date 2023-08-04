# Restful API

**REST**ful（**RE**presentational **S**tate **T**ransfer，表征性状态转移）

它是一种设计风格，提供了一组设计原则和约束参考。



关键点：

* 资源：在RESTful API中，一切皆资源。每个资源都有唯一的标识符（URI）来表示，并且可以通过HTTP方法对其进行操作
* 动作：通过简单的HTTP协议和方法对资源进行操作，如GET（获取资源）、POST（创建资源）、PUT（更新资源）、DELETE（删除资源）等。



实际开发中暴露的弊端：

* 版本管理：API都是依托于URL，一旦暴露出去很难改变，这也是实际开发中好多API前面会有/v1、/v2的原因

至于无状态、安全性、性能等问题，这些都是所依托的协议（比如HTTP）本身的问题，和RESTful这种设计风格并没有关系。



参考：

* [https://restfulapi.net/](https://restfulapi.net/)
* [https://apifox.com/blog/a-cup-of-tea-time-to-understand-restful-api/?https://www.apifox.cn/?utm\_source=google\_search\&utm\_medium=ads\_sa\&gclid=EAIaIQobChMIxJirhuzBgAMV6oNLBR162g9lEAAYASAAEgJv5vD\_BwE](https://apifox.com/blog/a-cup-of-tea-time-to-understand-restful-api/?https://www.apifox.cn/?utm\_source=google\_search\&utm\_medium=ads\_sa\&gclid=EAIaIQobChMIxJirhuzBgAMV6oNLBR162g9lEAAYASAAEgJv5vD\_BwE)
