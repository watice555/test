# git设置

## 设置git的用户名和邮箱

用户级别设置
```
git config --global user.name "watice"
git config --global user.email "w1825692103@gmail.com"
```
查询
```
git config --global --list
```

## git pull github 项目

```
git clone https://github.com/Hover-W/test.git
```

## 设置git代理

git config --global http.proxy http://127.0.0.1:7890
> 此为clash代理端口

---

# vs code 配置

```json
// 让预览时单个换行生效
"markdown.preview.breaks": true,
// 自动保存
"files.autoSave": "afterDelay",
"files.autoSaveDelay": 1000,
// 编辑器优化
"editor.wordWrap": "on",
"editor.fontSize": 16,
"editor.lineHeight": 1.8,
```
