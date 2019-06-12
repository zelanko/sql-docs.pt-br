---
title: PDO::quote | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b08ead32ba3c31f8f928c6e6dda051df1204073c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762016"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Processa uma cadeia de caracteres para uso em uma consulta, colocando a cadeia de caracteres de entrada entre aspas, conforme exigido pelo banco de dados do SQL Server subjacente. O PDO::quote insere um caractere de escape antes de caracteres especiais na cadeia de caracteres de entrada, usando um estilo de aspas adequado ao SQL Server.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*string*: a cadeia de caracteres a ser colocada entre aspas.  
  
$*parameter_type*: um símbolo opcional (inteiro) indicando o tipo de dados.  O padrão é PDO::PARAM_STR.  
  
## <a name="return-value"></a>Valor retornado  
Uma cadeia de caracteres entre aspas que pode ser passada para uma instrução SQL, ou false em caso de falha.  
  
## <a name="remarks"></a>Remarks  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
