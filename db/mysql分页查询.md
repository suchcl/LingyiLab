### mysql分页查询

公式

pageNumber: 当前页数

pageSize：每页的数据条数

```markdown
select * from tbname limit (pageNumber - 1) * pageSize;
```