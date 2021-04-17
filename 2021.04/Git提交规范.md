
# Git提交的Message格式
    type(scope): subject
    // 空一行
    body
    // 空一行
    footer
    
## type
    type为必填项，用于指定commit的类型，约定了feat、fix两个主要type，以及docs、style、build、refactor、perf五个特殊type，其余type暂不使用。
    
    # 主要type
    feat:     增加新功能
    fix:      修复bug
    
    # 特殊type
    docs:     只改动了文档相关的内容
    style:    不影响代码含义的改动，例如去掉空格、改变缩进、增删分号
    build:    构造工具的或者外部依赖的改动，例如maven、webpack、npm
    refactor: 代码重构时使用
    perf:     提高性能的改动
    
    # 其他type
    test:     添加测试或者修改现有测试
    revert:   代码版本回退
    ci:       与CI（持续集成服务）有关的改动
    chore:    不修改src或者test的其余修改，例如构建过程或辅助工具的变动
    
    当一次改动包括主要type与特殊type时，统一采用主要type。
    
    
## scope
    scope也为必填项，用于描述改动的范围，例如：
    core realname等模块名。
    如果一次commit修改多个模块，建议拆分成多次commit，以便更好追踪和维护。

## subject
    commit 目的的简短描述，不超过50个字符。
     以动词开头，使用第一人称现在时，比如change，而不是changed或changes
     第一个字母小写
     结尾不加句号（.）
     
## body
    body填写详细描述，主要描述改动之前的情况及修改动机，对于小的修改不作要求，但是重大需求、更新等必须添加body来作说明。

## footer
    一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接.
