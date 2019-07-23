---
title: sqlsrv_errors | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08879880e93307a496969b79c3aa05144f7aef62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015065"
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna informações estendidas sobre erros e/ou avisos da última operação do **sqlsrv** executada.  
  
A função **sqlsrv_errors** pode retornar informações sobre erros e/ou avisos se chamada com um dos valores de parâmetros especificado na seção Parâmetros abaixo.  
  
Por padrão, os avisos gerados em uma chamada para qualquer função do **sqlsrv** são tratados como erros. Se ocorrer um aviso em uma chamada para uma função do **sqlsrv** , ela retornará false. No entanto, os avisos correspondentes aos valores de SQLSTATE 01000, 01001, 01003 e 01S02 nunca são tratados como erros.  
  
A linha de código a seguir desativa o comportamento mencionado acima; um aviso gerado por uma chamada para uma função do **sqlsrv** não faz com que a função retorne false:  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
A linha de código a seguir restaura o comportamento padrão; os avisos são tratados como erros (com as exceções citadas acima):  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
Independentemente da configuração, os avisos só podem ser recuperados chamando **sqlsrv_errors** com o valor de parâmetro **SQLSRV_ERR_ALL** ou **SQLSRV_ERR_WARNINGS** (consulte a seção Parâmetros abaixo para obter mais detalhes).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$errorsAndOrWarnings*[OPCIONAL]: uma constante predefinida. Esse parâmetro pode assumir um dos valores listados na tabela a seguir:  
  
|Valor|Descrição|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Retorna erros e avisos gerados na última chamada da função **sqlsrv** .|  
|SQLSRV_ERR_ERRORS|Retorna erros gerados na última chamada da função **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Retorna avisos gerados na última chamada da função **sqlsrv** .|  
  
Se nenhum valor de parâmetro for fornecido, serão retornados os erros e avisos gerados pela última chamada para a função **sqlsrv** .  
  
## <a name="return-value"></a>Valor retornado  
Uma **matriz** de matrizes ou **null**. Cada **matriz** na **matriz** retornada contém três pares chave-valor. A tabela a seguir lista cada função e sua descrição:  
  
|Chave|Descrição|  
|-------|---------------|  
|SQLSTATE|Para erros originados no driver ODBC, o SQLSTATE retornado pelo ODBC. Para obter informações sobre valores de SQLSTATE para ODBC, consulte [Códigos de erro ODBC](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).<br /><br />Para erros originados nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], um SQLSTATE IMSSP.<br /><br />Para avisos originados nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], um SQLSTATE 01SSP.|  
|código|Para erros originados no SQL Server, o código de erro nativo do SQL Server.<br /><br />Para erros originados no driver ODBC, o código de erro retornado pelo ODBC.<br /><br />Para erros originados nos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], o código de erro do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] . Para obter mais informações, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).|  
|message|Uma descrição do erro.|  
  
Os valores da matriz também podem ser acessados com as chaves numéricas 0, 1 e 2. Se nenhum erro ou aviso ocorrer, será retornado **null** .  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir exibe os erros que ocorrem durante a execução de uma instrução com falha. (A instrução falha porque **InvalidColumName** não é um nome de coluna válido na tabela especificada.) O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
