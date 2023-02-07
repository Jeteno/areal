
# Secret  

## Local Setup
### Setup repo
```
$ npm install
```

### Setup DB
```
$ psql -U postgres -f ./db/createDB.sql
```

```
$ psql -d secret -U postgres -f ./db/createTables.sql
```

## Local Run
```
npm run start
```


