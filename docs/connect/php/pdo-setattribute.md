---
title: 'PDO:: setAttribute | Microsoft Docs'
ms.custom: 
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56f9ee96-e1d2-46cc-b137-38f06a251863
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8a7b4148d7c184570243a6665951f796c60b6ca0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
*$value*: o valor (tipo misturado).  
  
## <a name="return-value"></a>Valor de retorno  
Retorna true se for bem-sucedido; caso contrário, false.  
  
## <a name="remarks"></a>Comentários  
  
|Atributo|Processado por|Valores com suporte|Description|  
|-------------|----------------|--------------------|---------------|  
|PDO::ATTR_CASE|PDO|PDO::CASE_LOWER<br /><br />PDO::CASE_NATURAL<br /><br />PDO::CASE_UPPER|Especifica se serão usadas maiúsculas ou minúsculas nos nomes das colunas.<br /><br />PDO::CASE_LOWER faz com que os nomes das colunas sejam escritos em minúsculas.<br /><br />PDO::CASE_NATURAL (o padrão) exibe os nomes das colunas conforme são retornados pelo banco de dados.<br /><br />PDO::CASE_UPPER faz com que os nomes das colunas sejam escritos em maiúsculas.<br /><br />Esse atributo pode ser definido usando PDO::setAttribute.|  
|PDO::ATTR_DEFAULT_FETCH_MODE|PDO|Consulte a documentação do PDO.|Consulte a documentação do PDO.|  
|PDO::ATTR_ERRMODE|PDO|PDO::ERRMODE_SILENT<br /><br />PDO::ERRMODE_WARNING<br /><br />PDO::ERRMODE_EXCEPTION|Especifica como o driver relata falhas.<br /><br />PDO::ERRMODE_SILENT (o padrão) define os códigos e as informações de erro.<br /><br />PDO::ERRMODE_WARNING gera E_WARNING.<br /><br />PDO::ERRMODE_EXCEPTION faz com que uma exceção seja gerada.<br /><br />Esse atributo pode ser definido usando PDO::setAttribute.|  
|PDO::ATTR_ORACLE_NULLS|PDO|Consulte a documentação do PDO.|Especifica como os valores nulos devem ser retornados.<br /><br />PDO::NULL_NATURAL não faz nenhuma conversão.<br /><br />PDO::NULL_EMPTY_STRING converte uma cadeia de caracteres vazia em nulo.<br /><br />PDO::NULL_TO_STRING converte nulo em uma cadeia de caracteres vazia.|  
|PDO::ATTR_STATEMENT_CLASS|PDO|Consulte a documentação do PDO.|Define a classe de instrução que o usuário forneceu derivada de PDOStatement.<br /><br />Requer `array(string classname, array(mixed constructor_args))`.<br /><br />Para obter mais informações, consulte a documentação do PDO.|  
|PDO::ATTR_STRINGIFY_FETCHES|PDO|true ou false|Converte valores numéricos em cadeias de caracteres ao recuperar dados.|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|1 para o limite de memória do PHP.|Configura o tamanho do buffer que contém o conjunto de resultados.<br /><br />O padrão é 10.240 KB (10 MB).<br /><br />Para obter mais informações sobre consultas que criam um cursor do lado do cliente, consulte [tipos de Cursor &#40; Driver PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true<br /><br />false|Especifica a execução direta ou preparada da consulta. Para obter mais informações, consulte [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|PDO::SQLSRV_ENCODING_UTF8<br /><br />PDO::SQLSRV_ENCODING_SYSTEM.|Define a codificação do conjunto de caracteres usada pelo driver para se comunicar com o servidor.<br /><br />Não há suporte para PDO::SQLSRV_ENCODING_BINARY.<br /><br />O padrão é PDO::SQLSRV_ENCODING_UTF8.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|true ou false|Manipula numéricas buscas de colunas com tipos numéricos do SQL (bit, inteiro, smallint, tinyint, float ou real).<br /><br />Quando o sinalizador de opção de conexão ATTR_STRINGIFY_FETCHES está ativado, o valor de retorno é uma cadeia de caracteres até mesmo quando SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está ativado.<br /><br />Quando o tipo PDO retornado na coluna de associação for PDO_PARAM_INT, o valor de retorno de uma coluna de inteiros é um int, mesmo se SQLSRV_ATTR_FETCHES_NUMERIC_TYPE está desativado.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|inteiro|Define o tempo limite da consulta em segundos.<br /><br />O padrão é 0, o que significa que o driver aguardará resultados indefinidamente.<br /><br />Números negativos não são permitidos.|  
|PDO::SQLSRV_CLIENT_BUFFER_MAX_SIZE|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]|inteiro|Define o tamanho do buffer de consulta.<br /><br />O padrão é 0, que indica um tamanho do buffer ilimitado.<br /><br />Números negativos não são permitidos.<br /><br />Para obter mais informações sobre consultas que criam um cursor do lado do cliente, consulte [tipos de Cursor &#40; Driver PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
  
O PDO processa alguns atributos predefinidos e requer que o driver processe outros. Todos os atributos personalizados e opções de conexão são processados pelo driver. Um atributo sem suporte, opção de conexão ou valor sem suporte será relatado de acordo com a configuração de PDO:: attr_errmode.  
  
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
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

