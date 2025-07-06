# DataX

**DataX** is a lightweight .NET library for building local, file-based, structured data storage systems without a full database engine. It is part of the Next.Core suite.

---

## ✨ Features
- Define tables with custom schemas (headers, data types, roles)
- Support for primary keys and relations (OneToOne, OneToMany)
- CRUD operations for rows and columns
- Simple include (join-like) functionality
- File-based persistence (save/load)
- Extensible relation model

---

## 📦 Concepts
- **XTable**: Represents a table with schema and rows
- **XHeader**: Defines a column (name, data type, role)
- **Row**: Data record with key/value columns
- **XRelation**: Defines relations between tables
- **XDatabase**: Container for multiple tables

---

## 🔨 Example Usage

```csharp
using Next.Core.DataX;

string path = Path.Combine(Environment.CurrentDirectory, "MyDb.context");
string connectionString = $@"Database='{path}'; Username='Admin'; Password='1234';";

// Create new database context
DataServiceX.CreateDbContext(connectionString);

// Connect and use
using (var db = DataServiceX.Connect(connectionString))
{
    var users = db.GetTable("User");
    users.InsertRow(users.Counter(), "Ali", "1234", "admin@gmail.com", "0");

    var roles = db.GetTable("Role");
    roles.InsertRow(roles.Counter(), "Admin");

    foreach (var row in users.Rows)
    {
        foreach (var column in row.GetColumns())
        {
            Console.WriteLine($"{column.Key}: {column.Value}");
        }
        Console.WriteLine("----------------------");
    }
}
```

# 📌 Persistence

DataX stores tables as **plain text files** for easy portability and transparency:

- **Schema and settings**: Column definitions, data types, roles.
- **Rows with values**: All data records in a readable format.
- **Relations in separate files**: Defines OneToOne, OneToMany, and other links.

This design enables **manual inspection and editing** without special tools.

---

# ✅ Use Cases

- Embedded apps needing **structured local storage**
- **Configurable business rules** with join-like queries
- **Offline-first desktop utilities**
- **Rapid prototyping** without a server database

---

# 📜 License

Part of the **Next.Core 1.0** release.  
Intended for **professional development use**.  
Licensing terms may depend on **deployment model** and **organizational agreements**.

