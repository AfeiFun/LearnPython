1. 在用户目录下的.bashrc是用来设置每次用该用户打开bash时自动运行的操作。
    ```bash
    #添加欢迎词
    echo "Hi~"

    # 设置PATH
    export PATH="local的绝对路径:$PATH"

    #重新载入.bashrc文件
    source ~/.bashrc
    ```
2. 激活虚拟环境 `source activate`，在activate的目录中运行该脚本。
3. 推出虚拟环境,直接输入`deactivate`。
3. `source` 命令的作用：在当前bash环境下读取并执行FileName中的命令：`source activate`,也可以用`.`来代替，比如`. filename`（中间有空格）。
