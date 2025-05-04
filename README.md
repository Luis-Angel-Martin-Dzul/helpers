# helpers

## Configuración de la Conexión a la Base de Datos

Asegúrate de configurar correctamente la cadena de conexión en tu archivo `appsettings.json`:

```json
"ConnectionStrings": {
  "DB": "Server=YourServerName\\SQLEXPRESS; Database=YourDatabaseName; Integrated Security=true; Persist Security Info=False; TrustServerCertificate=True"
}
```

## Scaffolding de la base de datos (SQL Server)
```cmd
dotnet ef dbcontext scaffold "Server=MASTERCHIS\SQLEXPRESS;Database=Kikis_DB;Integrated Security=True;TrustServerCertificate=True" Microsoft.EntityFrameworkCore.SqlServer -o Data
```

## Generar token aleatorio (C#)
```cmd
public static string GenerateRandomString(int length) {
    
    string validChars = 
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ" +
        "abcdefghijklmnopqrstuvwxyz" +
        "0123456789";

    Random random = new Random();
    StringBuilder password = new StringBuilder();

    for (int i = 0; i < length; i++) {
        int index = random.Next(validChars.Length);

        password.Append(validChars[index]);
    }

    return password.ToString();
}
```

## Encriptar con SHA-256
```cmd
public static string EncodeSHA256(string encode) {
    SHA256 sha256 = SHA256.Create();
    ASCIIEncoding encoding = new ASCIIEncoding();
    byte[]? stream = null;
    StringBuilder sb = new StringBuilder();
    stream = sha256.ComputeHash(encoding.GetBytes(encode));
    for(int i = 0; i < stream.Length; i++)
        sb.AppendFormat("{0:x2}", stream[i]);
    return sb.ToString();
}
```

## Encriptar con Base64 (No seguro) 
```cmd
public static string EncodeBase64(string encode) {

    var bytes = Encoding.UTF8.GetBytes(encode);
    string base64 = Convert.ToBase64String(bytes)
        .Replace("/", ".")
        .Replace("=", "_");
    return base64;
}
```
## Desencriptar con Base64 (No seguro) 
```cmd
public static string DecodeBase64(string decode) {

    decode = decode
        .Replace(".", "/")
        .Replace("_", "=");

    var bytes = Convert.FromBase64String(decode);
    var plainText = Encoding.UTF8.GetString(bytes);

    return plainText;
}
```

