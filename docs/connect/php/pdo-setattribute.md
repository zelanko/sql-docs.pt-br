---
title: PDO::setAttribute | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5402742793877d8e022eff4d207c49cf31f42256
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761796"
---
# <a name="pdosetattribute"></a>PDO::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Define um atributo de PDO preestabelecido ou um atributo de driver personalizado.  
  
## <a name="syntax"></a>Sintaxe  
  
```
bool PDO::setAttribute ( $attribute, $value );  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$attribute*: o atributo a ser definido. Consulte a seção Comentários para obter uma lista de atributos com suporte.  
  
*$value*: o valor (tipo misto).  
  
## <a name="return-value"></a>Valor retornado  
Retorna true se for bem-sucedido; caso contrário, false.  
  
## <a name="remarks"></a>Remarks  
  
|attribute|Processado por|Valores com suporte|Descrição|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|Especifica se serão usadas maiúsculas ou minúsculas nos nomes das colunas.<br /><br />PDO::CASE_LOWER faz com que os nomes das colunas sejam escritos em minúsculas.<br /><br />PDO::CASE_NATURAL (o padrão) exibe os nomes das colunas conforme são retornados pelo banco de dados.<br /><br />PDO::CASE_UPPER faz com que os nomes das colunas sejam escritos em maiúsculas.<br /><br />Esse atributo pode ser definido usando PDO::setAttribute.|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|Consulte a documentação do PDO.|Consulte a documentação do PDO.|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|Especifica como o driver relata as falhas.<br /><br />PDO::ERRMODE_SILENT (o padrão) define os códigos e as informações de erro.<br /><br />PDO::ERRMODE_WARNING gera E_WARNING.<br /><br />PDO::ERRMODE_EXCEPTION faz com que uma exceção seja gerada.<br /><br />Esse atributo pode ser definido usando PDO::setAttribute.|  
|PDO::ATTR_ORACLE_NULLS|PDO|Consulte a documentação do PDO.|Especifica como os valores nulos devem ser retornados.<br /><br />PDO::NULL_NATURAL não faz nenhuma conversão.<br /><br />PDO::NULL_EMPTY_STRING converte uma cadeia de caracteres vazia em nulo.<br /><br />PDO::NULL_TO_STRING converte nulo em uma cadeia de caracteres vazia.|  
|PDO::ATTR_STATEMENT_CLASS|PDO|Consulte a documentação do PDO.|Define a classe de instrução que o usuário forneceu derivada de PDOStatement.<br /><br />Requer `array(string classname, array(mixed constructor_args))`.<br /><br />Veja a documentação do PDO para obter mais informações.|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true ou false|Converte valores numéricos em cadeias de caracteres ao recuperar dados.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 para o limite de memória do PHP.|Define o tamanho do buffer que contém o conjunto de resultados ao usar um cursor do lado do cliente.<br /><br />O padrão é 10.240 KB, se não for especificado no arquivo php.ini.<br /><br />Zero e números negativos não são permitidos.<br /><br />Para obter mais informações sobre as consultas que criam um cursor do lado do cliente, veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|Um inteiro entre 0 e 4 (inclusive)|Especifica o número de casas decimais ao formatar valores monetários buscados.<br /><br />Qualquer inteiro negativo ou um valor maior que 4 será ignorado.<br /><br />Esta opção só funciona quando PDO::SQLSRV_ATTR_FORMAT_DECIMALS é verdadeiro.<br /><br />Esta opção também pode ser definida no nível de instrução. Nesse caso, a opção de nível de instrução substitui essa.<br /><br />Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true ou false|Especifica a execução direta ou preparada da consulta. Para obter mais informações, consulte [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|Define a codificação do conjunto de caracteres usada pelo driver para se comunicar com o servidor.<br /><br />Não há suporte para PDO::SQLSRV_ENCODING_BINARY.<br /><br />O padrão é PDO::SQLSRV_ENCODING_UTF8.|  
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true ou false|Especifica quando recuperar tipos de data e hora como objetos de [DateTime PHP](http://php.net/manual/en/class.datetime.php). Se for deixado como false, o comportamento padrão é retorná-los como cadeias de caracteres.<br /><br />Esta opção também pode ser definida no nível de instrução. Nesse caso, a opção de nível de instrução substitui essa.<br /><br />Para saber mais, confira [Como recuperar tipos de data e hora como objetos DateTime PHP usando o driver PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true ou false|Lida com buscas numéricas de colunas com tipos numéricos do SQL (bit, inteiro, smallint, tinyint, float ou real).<br /><br />Quando o sinalizador de opção de conexão ATTR_STRINGIFY_FETCHES está ativado, o valor de retorno é uma cadeia de caracteres, mesmo quando SQLSRV_ATTR_FETCHES_NUMERIC_TYPE estiver ativado.<br /><br />Quando o tipo PDO retornado na coluna de associação for PDO_PARAM_INT, o valor de retorno de uma coluna de números inteiros é int, mesmo se SQLSRV_ATTR_FETCHES_NUMERIC_TYPE estiver desativado.|  
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true ou false|Especifica quando é apropriado adicionar zeros iniciais em cadeias de caracteres decimais. Se definida, essa opção habilita a opção PDO::SQLSRV_ATTR_DECIMAL_PLACES para formatação de tipos de moedas. Se for deixado como false, será usado o comportamento padrão de retornar a precisão exata e omitir zeros para valores menores do que 1.<br /><br />Esta opção também pode ser definida no nível de instrução. Nesse caso, a opção de nível de instrução substitui essa.<br /><br />Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|inteiro|Define o tempo limite da consulta em segundos.<br /><br />O padrão é 0, o que significa que o driver aguardará resultados indefinidamente.<br /><br />Números negativos não são permitidos.|  
  
O PDO processa alguns atributos predefinidos e requer que o driver processe outros. Todos os atributos personalizados e opções de conexão são processados pelo driver. Um atributo sem suporte, opção de conexão ou valor sem suporte será relatado de acordo com a configuração de PDO::ATTR_ERRMODE.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra como definir o atributo PDO::ATTR_ERRMODE.  
  
```  
<?php  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
  
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
  
   $attributes1 = array( "ERRMODE" );  
   foreach ( $attributes1 as $val ) {  
      echo "PDO::ATTR_$val: ";  
      var_dump ($conn->getAttribute( constant( "PDO::ATTR_$val" ) ));  
   }  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
