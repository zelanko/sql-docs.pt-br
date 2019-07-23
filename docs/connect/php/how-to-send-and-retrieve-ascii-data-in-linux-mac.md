---
title: 'Como: enviar e recuperar dados ASCII no Linux e macOS (SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 9edd73f5ef01d1d3f22db78400cc3c204efe1379
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251902"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>Como enviar e recuperar dados ASCII em Linux e macOS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este artigo pressupõe que as localidades ASCII (não UTF-8) foram geradas ou instaladas em seus sistemas Linux ou macOS. 

Para enviar ou recuperar conjuntos de caracteres ASCII para o servidor:  

1.  Se a localidade desejada não for o padrão no ambiente do sistema, certifique-se de `setlocale(LC_ALL, $locale)` invocar antes de fazer a primeira conexão. A função PHP setlocalment () altera a localidade somente para o script atual e, se for invocada depois de fazer a primeira conexão, ela poderá ser ignorada.
 
2.  Ao usar o driver sqlsrv, você pode especificar `'CharacterSet' => SQLSRV_ENC_CHAR` como uma opção de conexão, mas essa etapa é opcional porque é a codificação padrão.

3.  Ao usar o driver PDO_SQLSRV, há duas maneiras. Primeiro, ao fazer a conexão, defina `PDO::SQLSRV_ATTR_ENCODING` como `PDO::SQLSRV_ENCODING_SYSTEM` (para obter um exemplo de como definir uma opção de conexão, consulte [PDO:: __construct](../../connect/php/pdo-construct.md)). Como alternativa, depois de conectado com êxito, adicione esta linha`$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
Quando você especifica a codificação de um recurso de conexão (em SQLSRV) ou objeto de conexão (PDO_SQLSRV), o driver pressupõe que as outras cadeias de caracteres de opção de conexão usam essa mesma codificação. Também pressupõe-se que o nome do servidor e as cadeias de caracteres de consulta usem o mesmo conjunto de caracteres.  
  
A codificação padrão para o driver PDO_SQLSRV é UTF-8 (PDO:: SQLSRV_ENCODING_UTF8), diferentemente do driver SQLSRV. Para obter mais informações sobre essas constantes, veja [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). 
  
## <a name="example"></a>Exemplo  
Os exemplos a seguir demonstram como enviar e recuperar dados ASCII usando os drivers do PHP para SQL Server especificando uma localidade específica antes de fazer a conexão. As localidades em várias plataformas Linux podem ser nomeadas de forma diferente das mesmas localidades no macOS. Por exemplo, a localidade ISO-8859-1 (Latin 1) dos EUA `en_US.ISO-8859-1` está no Linux enquanto estiver no MacOS, `en_US.ISO8859-1`o nome é.
  
Os exemplos pressupõem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que o esteja instalado em um servidor. Toda a saída é gravada no navegador quando os exemplos são executados do navegador.  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>Consulte Também  
[Recuperando dados](../../connect/php/retrieving-data.md)  
[Trabalhando com dados](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
UTF-8[atualizando &#40;dados drivers da Microsoft para PHP&#41; para SQL Server](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
