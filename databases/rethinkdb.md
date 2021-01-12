# RethinkDB Cheat Sheet

## Create database

```
r.dbCreate('mydb')
```

## List databases

```
r.dbList()
```

## Drop database

```
r.dbDrop('test')
```

## Create table

```
r.db('mydb').tableCreate('users')
```

## Delete table

```
r.db('mydb').table("test").delete()
```

## Insert record

```
r.db('mydb').table('users').insert({
		name: 'Brad Traversy',
		city: 'Boston',
		age: 37
	}
)
```

## Insert records (Array or object)

```
r.db('mydb').table('users').insert([
		{name: 'John Doe', city: 'Miami', age: 34},
		{name: 'Sara Wilson', city: 'Boston', age: 28},
		{name: 'Steve Smith', city: 'Detroit', age: 49},
		{name: 'Jen Williams', city: 'Miami', age: 35}
])
```

## Get records

```
r.db('mydb').table('users')
```

## Filter records

```
r.db('mydb').table('users').filter({
		city: 'Boston'
})
```

## Select specific fields

```
r.db('mydb').table('users').pluck('name')
```

## Order By

```
r.db('mydb').table('users').orderBy(r.desc('name'))
```

## Pluck & order by

```
r.db('mydb').table('users').filter({
	'city': 'Boston'
}).orderBy(
	r.desc('name')
).pluck('name')
```

## Limit records

```
r.db('mydb').table('users').limit(2)
```

## Count

```
r.db('mydb').table("users").count()
```

## Distinct

```
r.db('mydb').table("users").pluck("city").distinct()
```

## Greater & less than

```
r.db('mydb').table("users").filter(r.row('age').gt(35))
r.db('mydb').table("users").filter(r.row('age').gte(35))
r.db('mydb').table("users").filter(r.row('age').lt(35))
```

## Update record

```
r.db('mydb').table("users").filter({
		id: '592502cc-a84e-442d-a45f-24ebc344d8cf'
}).update({
    "city": 'Miami'
})
```

## Delete record

```
r.db('mydb').table("users").filter({
		id: '592502cc-a84e-442d-a45f-24ebc344d8cf'
}).delete()
```

## Joins

## Create and insert data for second table

```
r.db('mydb').table('tasks')
```

```
r.db('mydb').table('tasks').insert([
		{user_id: '50ea168e-400f-4ad6-9e6e-a09451b9a837', text: 'Task One'},
		{user_id: 'f4fdffdc-30f7-4b4b-895d-c4a362864441', text: 'Task Two'},
		{user_id: '50ea168e-400f-4ad6-9e6e-a09451b9a837', text: 'Task Three'},
		{user_id: '50ea168e-400f-4ad6-9e6e-a09451b9a837', text: 'Task Four'}
])
```

## Join tables

```
r.db('mydb').table("tasks").eqJoin("user_id", r.db('mydb').table("users")).zip()
```

## zip() will merge the user in the task, overwriting fields in case of conflict

```
r.db('mydb').table("tasks").eqJoin("user_id", r.db('mydb').table("users")).zip()
```
