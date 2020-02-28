### Ontology Web Language

### Semantic Web

- 非常有利于信息共享:
  - 传统关系型数据库共享信息，如果两张表都是描述Person，但是schema不同，就需要将源数据更具目标数据的schema进行转换，可能会丢失信息
  - Semantic Web：源本体定义了概念以及关系，目标本体也定义了概念以及关系，只需要做本体对齐，将目标本体中的概念及关系与源本体的概念及关系对齐（定义一些equivalentclass和subpropertyof等等），就可以完成信息共享。对于源本体用不到的信息，依然会存储在本体中，不会丢失。

- 编辑工具：protege，cyc，kano2
- 推理工具：jena，pellet，hermit
- 