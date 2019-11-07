# 官方文档
https://gerrit.googlesource.com/git-repo/+/HEAD/docs/manifest-format.md

# 解释下常用的各节点：
## remote
远程仓库地址配置，可以多个。
- name: 名字，也用于子仓库的 git remote 名称（.git/config 里的 remote）
- alias: 别名，可省略，建议设为 origin， 设置了那么子仓库的 git remote 即为此名，方便不同的 name 下可以最终设置生成相同的 remote 名称
- fetch: 仓库地址前缀，即 project 的仓库地址为: remote.fetch + project.name
- pushurl: 一般可省略，省略了则直接用 fetch
- review: Gerrit code review 的地址，如果没有用 Gerrit 则不需要配置（也就不能用 repo upload 命令了）
- revision: 使用此 remote 的默认分支

## project
子项目仓库配置，可以多个。
- path: repo sync 同步时，相对于根目录的子仓库文件夹路径
- name: 子仓库的 git 仓库名称
- group: 分组
- revision: 使用的分支名
- clone-depth: 仓库同步 Git 的 depth

### copyfile
project 的子节点属性.
- src: project 下的相对路径
- dest: 整个仓库根路径下的相对路径

### linkfile
project 的子节点属性，类似 copyfile，只是把复制文件变为创建链接文件。

### default
project 没有设置属性时会使用的默认配置，常用的是 remote 和 revision。