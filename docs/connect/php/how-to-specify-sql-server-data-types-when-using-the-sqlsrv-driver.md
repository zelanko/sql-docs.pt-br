---
title: Como especificar tipos de dados do SQL Server usando o Driver SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b9ddb359c34e929247357713c5c48035a3eed9a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993359"
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>Como especificar tipos de dados do SQL Server usando o Driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico demonstra como usar o driver SQLSRV para especificar o tipo de dados do SQL Server para dados enviados ao servidor. Este tópico não se aplica ao usar o driver PDO_SQLSRV.  
  
Para especificar o tipo de dados do SQL Server, você deve usar a matriz opcional *$params* ao preparar ou executar uma consulta que insere ou atualiza dados. Para obter detalhes sobre a estrutura e a sintaxe da matriz *$params* , consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
As etapas a seguir resumem como especificar o tipo de dados do SQL Server ao enviar dados para o servidor:  
  
> [!NOTE]  
> Se nenhum tipo de dados do SQL Server for especificado, serão usados os tipos padrão. Para obter informações sobre os tipos de dados padrão do SQL Server, consulte [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md).  
  
1.  Defina uma consulta Transact-SQL que insere ou atualiza dados. Use pontos de interrogação (?) como espaços reservados para valores de parâmetro na consulta.  
  
2.  Inicialize ou atualize as variáveis do PHP correspondentes aos espaços reservados na consulta Transact-SQL.  
  
3.  Crie a matriz *$params* a ser usada na preparação ou na execução da consulta. Observe que, ao especificar o tipo de dados do SQL Server, cada elemento da matriz *$params* também deve ser uma matriz.  
  
4.  Especifique o tipo de dados do SQL Server desejado usando a constante **SQLSRV_SQLTYPE_&#42;** adequada como o quarto parâmetro em cada submatriz da matriz *$params*. Para obter uma lista completa das constantes **SQLSRV_SQLTYPE_&#42;** , confira a seção SQLTYPEs de [Constantes &#40;Microsoft Drivers para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). Por exemplo, no código a seguir, *$changeDate*, *$rate*e *$payFrequency* são especificados respectivamente com os tipos do SQL Server **datetime**, **money**e **tinyint** na matriz *$params* . Como nenhum tipo do SQL Server é especificado para *$employeeId* , que é inicializado como um inteiro, é usado o tipo padrão do SQL Server **integer** .  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir insere dados na tabela *HumanResources.EmployeePayHistory* do banco de dados do AdventureWorks. Os tipos do SQL Server são especificados para os parâmetros *$changeDate*, *$rate*, e *$payFrequency* . O tipo padrão do SQL Server é usado para o parâmetro *$employeeId* . Para verificar se os dados foram inseridos com êxito, os mesmos dados são recuperados e exibidos.  
  
Este exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the query. */  
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Recuperando dados](../../connect/php/retrieving-data.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[Como especificar tipos de dados do PHP](../../connect/php/how-to-specify-php-data-types.md)

[Convertendo tipos de dados](../../connect/php/converting-data-types.md)

[Como enviar e recuperar dados UTF-8 usando o suporte interno a UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
