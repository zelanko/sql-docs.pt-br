---
title: 'Pdostatement:: setAttribute | Microsoft Docs'
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbbb53da59f463c8dc601963f02b5b77ef6ec4b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Define um valor de atributo, seja um atributo de PDO preestabelecido ou um atributo de driver personalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*atributo*: um inteiro, uma das constantes * ou PDO::SQLSRV_ATTR_\* constantes. Consulte a seção Comentários para obter uma lista de atributos disponíveis.  
  
$*valor*: O valor (misto) a ser definido para o $ especificado*atributo*.  
  
## <a name="return-value"></a>Valor de retorno  
TRUE se for bem-sucedido; caso contrário, FALSE.  
  
## <a name="remarks"></a>Remarks  
A tabela a seguir contém a lista dos atributos disponíveis:  
  
|attribute|Valores|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 para o limite de memória do PHP.|Configura o tamanho do buffer que contém o conjunto de resultados de um cursor do lado do cliente.<br /><br />O padrão é 10.240 KB (10 MB).<br /><br />Para obter mais informações sobre cursores do lado do cliente, consulte [tipos de Cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO:: sqlsrv_encoding_utf8 (padrão)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Define a codificação do conjunto de caracteres a ser usada pelo driver para se comunicar com o servidor.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true ou false|Manipula numéricas buscas de colunas com tipos numéricos do SQL (bit, inteiro, smallint, tinyint, float ou real).<br /><br />Quando o sinalizador de opção de conexão ATTR_STRINGIFY_FETCHES está ativado, o valor de retorno é uma cadeia de caracteres até mesmo quando SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está ativado.<br /><br />Quando o tipo PDO retornado na coluna de associação for PDO_PARAM_INT, o valor de retorno de uma coluna de inteiros é um int, mesmo se SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está desativado.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|Define o tempo limite da consulta em segundos.<br /><br />Por padrão, o driver aguardará resultados indefinidamente. Números negativos não são permitidos.<br /><br />0 significa “sem tempo limite”.|  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
