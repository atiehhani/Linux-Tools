# MongoDB Commands Reference

## Authentication

**Login as "support" user to `thirdparty` database:**
```bash
mongo -u support -p --host 192.168.243.75 --port 27017 thirdparty
```

**Login as "admin" user to default database:**
```bash
mongo -u admin -p --host 192.168.243.75 --port 27017
```

---

## Database Operations

*   **Show all databases:**
    ```javascript
    show dbs
    ```
*   **Switch to a specific database:**
    ```javascript
    use <your_database_name>
    ```
*   **List all collections (tables) in the current database:**
    ```javascript
    show collections
    ```

---

## User Management

**List users defined in a specific database (with roles):**
```javascript
use <your_database_name>
db.getUsers()
```

**List all users (across all databases):**
```javascript
db.system.users.find()
```

**Create a user for `thirdparty` database:**
```javascript
db.createUser({ 
  user: "aref", 
  pwd: "aref", 
  roles: [{ role: "readWrite", db: "thirdparty" }] 
})
```

**Reset a user's password:**
1. Login as `admin`
2. Switch to the target DB: `use <your_database_name>`
3. List users to identify the target: `db.getUsers()`
4. Change the password:
   ```javascript
   db.changeUserPassword("username", "new_password")
   ```
