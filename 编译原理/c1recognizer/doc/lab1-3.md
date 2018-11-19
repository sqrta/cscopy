# Lab1-3
## 编写补全syntax_tree_builder.cpp文件遇到的问题
需要修改Parser.g4文件，原来是

    block: LeftBrace (stmt | decl)* RightBrace;
修改为

    block: LeftBrace blockitem* RightBrace;
    blockitem: stmt | decl;
因为如果使用原来的版本，antlr4为blockContext部分提供的api会返回stmt的列表和decl的列表，但是会丢失次序信息，即无法确定两个列表混合到一起组成blocklist时的次序。如此修改后会统一返回blockitem列表，即得到了次序信息后再对是stmt还是decl分开处理