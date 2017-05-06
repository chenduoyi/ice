# sed 文本批量替换

格式: sed -i "s/查找字段/替换字段/g" `grep 查找字段 -rl 路径`

```
sed -i "s/origin key words/new key words/g" \`grep origin key words -rl /home/wwwroot/\`
```

注意 : 反引号 \`\`
