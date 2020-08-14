1. 在用户目录下的.bashrc是用来设置每次用该用户打开bash时自动运行的操作。
    ```bash
    #添加欢迎词
    echo "Hi~"

    # 设置PATH
    export PATH="local的绝对路径:$PATH"

    #重新载入.bashrc文件
    source ~/.bashrc
    ```