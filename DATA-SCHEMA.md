# Fitfolio 数据结构

## IndexedDB

- 数据库名称：`wardrobe_pocket_indexeddb_v1`
- 数据库版本：`1`
- 对象仓库：`items`、`outfits`
- 两个对象仓库都使用 `id` 作为 `keyPath`

### items

单品记录包含：

- `id`
- `name`
- `category`
- `material`
- `purchaseDate`
- `price`
- `seasons`
- `location`
- `note`
- `imageBlob`：浏览器中的图片 Blob
- `createdAt`
- `updatedAt`

### outfits

穿搭记录包含：

- `id`
- `name`
- `seasons`
- `note`
- `itemIds`：仅引用 `items` 中已经存在的单品 ID
- `createdAt`
- `updatedAt`

## JSON 备份

当前备份格式：

```json
{
  "format": "fitfolio-backup",
  "version": 1,
  "app": "Fitfolio",
  "exportedAt": "ISO-8601 时间",
  "database": {
    "name": "wardrobe_pocket_indexeddb_v1",
    "version": 1
  },
  "items": [],
  "outfits": []
}
```

导出时，`imageBlob` 会转换成 `imageDataUrl`。导入时会验证图片必须是 JPEG、PNG、WebP 或 GIF 的 Base64 data URL，然后重新转换为 Blob。

如果未来修改数据库或备份格式，应保留旧版本的迁移逻辑，不能通过清空用户数据库来解决兼容问题。

