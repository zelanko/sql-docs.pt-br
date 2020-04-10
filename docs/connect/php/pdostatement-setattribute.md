---
title: PDOStatement::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5c5c0670ceb9725c04a63a59a09b25cf72c810
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925253"
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Define um valor de atributo, seja um atributo de PDO preestabelecido ou um atributo de driver personalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>parâmetros  
$*attribute*: um inteiro, uma das constantes PDO::ATTR_* ou PDO::SQLSRV_ATTR_\*. Consulte a seção Comentários para obter uma lista de atributos disponíveis.  
  
$*value*: o valor (misto) a ser definido para o $*attribute* especificado.  
  
## <a name="return-value"></a>Valor retornado  
TRUE se for bem-sucedido; caso contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
A tabela a seguir contém a lista dos atributos disponíveis:  
  
|Atributo|Valores|DESCRIÇÃO|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 para o limite de memória do PHP.|Configura o tamanho do buffer que contém o conjunto de resultados de um cursor do lado do cliente.<br /><br />O padrão é 10.240 KB (10 MB).<br /><br />Para obter mais informações sobre os cursores do lado do cliente, veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DATA_CLASSIFICATION|true ou false|Especifica se os metadados de classificação de dados devem ser recuperados ao chamar [PDOStatement::getColumnMeta](../../connect/php/pdostatement-getcolumnmeta.md). O padrão é false.|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|Um inteiro entre 0 e 4 (inclusive)|Especifica o número de casas decimais ao formatar valores monetários buscados.<br /><br />Qualquer inteiro negativo ou um valor maior que 4 será ignorado.<br /><br />Esta opção só funciona quando PDO::SQLSRV_ATTR_FORMAT_DECIMALS é verdadeiro.<br /><br />Esta opção também pode ser definida no nível de conexão. Nesse caso, esta opção substitui a opção de nível de conexão.<br /><br />Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO::SQLSRV_ENCODING_UTF8 (padrão)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Define a codificação do conjunto de caracteres a ser usada pelo driver para se comunicar com o servidor.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|true ou false|Especifica quando recuperar tipos de data e hora como objetos de [DateTime PHP](http://php.net/manual/en/class.datetime.php). Se for deixado como false, o comportamento padrão é retorná-los como cadeias de caracteres.<br /><br />Esta opção também pode ser definida no nível de conexão. Nesse caso, esta opção substitui a opção de nível de conexão.<br /><br />Para saber mais, confira [Como recuperar tipos de data e hora como objetos DateTime PHP usando o driver PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true ou false|Lida com buscas numéricas de colunas com tipos numéricos do SQL (bit, inteiro, smallint, tinyint, float ou real).<br /><br />Quando o sinalizador de opção de conexão ATTR_STRINGIFY_FETCHES está ativado, o valor de retorno é uma cadeia de caracteres, mesmo quando SQLSRV_ATTR_FETCHES_NUMERIC_TYPE estiver ativado.<br /><br />Quando o tipo PDO retornado na coluna de associação for PDO_PARAM_INT, o valor de retorno de uma coluna de números inteiros é int, mesmo se SQLSRV_ATTR_FETCHES_NUMERIC_TYPE estiver desativado.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|true ou false|Especifica quando é apropriado adicionar zeros à esquerda em cadeias de caracteres decimais. Se definida, essa opção habilita a opção PDO::SQLSRV_ATTR_DECIMAL_PLACES para formatação de tipos de moedas. Se for deixado como false, será usado o comportamento padrão de retornar a precisão exata e omitir zeros para valores menores do que 1.<br /><br />Esta opção também pode ser definida no nível de conexão. Nesse caso, esta opção substitui a opção de nível de conexão.<br /><br />Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).| 
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
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
