---
title: sqlsrv_errors | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9994273b04f7928826ca5f4c7997d51a548d488e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna estendidas de erro e/ou informações de aviso sobre a última **sqlsrv** operação realizada.  
  
O **sqlsrv_errors** função pode retornar o erro e/ou informações de aviso chamada com um dos valores de parâmetros especificados na seção parâmetros abaixo.  
  
Por padrão, os avisos gerados em uma chamada para qualquer função do **sqlsrv** são tratados como erros. Se ocorrer um aviso em uma chamada para uma função do **sqlsrv** , ela retornará false. No entanto, os avisos correspondentes aos valores de SQLSTATE 01000, 01001, 01003 e 01S02 nunca são tratados como erros.  
  
A linha de código a seguir desativa o comportamento mencionado acima; um aviso gerado por uma chamada para uma função do **sqlsrv** não faz com que a função retorne false:  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
A linha de código a seguir restaura o comportamento padrão; os avisos são tratados como erros (com as exceções citadas acima):  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
Independentemente da configuração, os avisos só podem ser recuperados chamando **sqlsrv_errors** com qualquer um de **SQLSRV_ERR_ALL** ou **SQLSRV_ERR_WARNINGS** (veja o valor do parâmetro Seção parâmetros abaixo para obter detalhes).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$errorsAndOrWarnings*[opcional]: uma constante predefinida. Esse parâmetro pode assumir um dos valores listados na tabela a seguir:  
  
|Valor|Description|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Retorna erros e avisos gerados na última chamada da função **sqlsrv** .|  
|SQLSRV_ERR_ERRORS|Retorna erros gerados na última chamada da função **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Retorna avisos gerados na última chamada da função **sqlsrv** .|  
  
Se nenhum valor de parâmetro for fornecido, serão retornados os erros e avisos gerados pela última chamada para a função **sqlsrv** .  
  
## <a name="return-value"></a>Valor de retorno  
Uma **matriz** de matrizes ou **null**. Cada **matriz** em retornado **matriz** contém três pares chave-valor. A tabela a seguir lista cada função e sua descrição:  
  
|Chave|Descrição|  
|-------|---------------|  
|SQLSTATE|Para erros originados no driver ODBC, o SQLSTATE retornado pelo ODBC. Para obter informações sobre valores de SQLSTATE para ODBC, consulte [Códigos de erro ODBC](http://go.microsoft.com/fwlink/?linkid=119618).<br /><br />Para erros originados nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], um SQLSTATE IMSSP.<br /><br />Para avisos originados nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], um SQLSTATE 01SSP.|  
|código|Para erros originados no SQL Server, o código de erro nativo do SQL Server.<br /><br />Para erros originados no driver ODBC, o código de erro retornado pelo ODBC.<br /><br />Para erros originados nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], o código de erro do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] . Para obter mais informações, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).|  
|message|Uma descrição do erro.|  
  
Os valores da matriz também podem ser acessados com as chaves numéricas 0, 1 e 2. Se nenhum erro ou aviso ocorrer, será retornado **null** .  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir exibe os erros que ocorrem durante a execução de uma instrução com falha. (A instrução falha porque **InvalidColumName** não é um nome de coluna válido na tabela especificada.) O exemplo supõe que SQL Server e o [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) banco de dados são instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  

