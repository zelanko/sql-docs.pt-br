---
title: 'Pdostatement:: Fetch | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4368e362-5bda-4da1-8462-33714683c39f
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f503ddd9d661d2b2bfa75a3c19219874f159c42
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementfetch"></a>PDOStatement::fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera uma linha de um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDOStatement::fetch ([ $fetch_style[, $cursor_orientation[, $cursor_offset]]] );  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*fetch_style*: um símbolo (inteiro) opcional especificando o formato dos dados da linha. Consulte a seção de comentários para a lista de valores possíveis para $*fetch_style*. O padrão é PDO::FETCH_BOTH. $*fetch_style* na busca método substituirá o $*fetch_style* especificada no método PDO:: Query.  
  
$*cursor_orientation*: um símbolo (inteiro) opcional que indica a linha a ser recuperada quando a instrução prepare especifica `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`. Consulte a seção de comentários para a lista de valores possíveis para $*cursor_orientation*. Consulte [PDO::prepare](../../connect/php/pdo-prepare.md) para obter um exemplo usando um cursor rolável.  
  
$*cursor_offset*: um símbolo opcional (inteiro) especificando a linha a ser buscada $*cursor_orientation* é fetch_ori_abs ou fetch_ori_rel e PDO:: attr_cursor é PDO:: cursor_scroll.  
  
## <a name="return-value"></a>Valor de retorno  
Um valor misto que retorna uma linha ou false.  
  
## <a name="remarks"></a>Comentários  
O cursor é avançado automaticamente quando a busca é chamada. A tabela a seguir contém a lista de possíveis $*fetch_style* valores.  
  
|$*fetch_style*|Description|  
|-------------------|---------------|  
|PDO::FETCH_ASSOC|Especifica uma matriz indexada pelo nome da coluna.|  
|PDO::FETCH_BOTH|Especifica uma matriz indexada pelo nome da coluna e ordem com base em zero. Esse é o padrão.|  
|PDO::FETCH_BOUND|Retorna true e atribui os valores conforme especificado por [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md).|  
|PDO::FETCH_CLASS|Cria uma instância e mapeia as colunas para propriedades nomeadas.<br /><br />Chame [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) antes de chamar a busca.|  
|PDO::FETCH_INTO|Atualiza uma instância da classe solicitada.<br /><br />Chame [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) antes de chamar a busca.|  
|PDO::FETCH_LAZY|Cria nomes de variáveis durante o acesso e cria um objeto sem nome.|  
|PDO::FETCH_NUM|Especifica uma matriz indexada por ordem de colunas com base em zero.|  
|PDO::FETCH_OBJ|Especifica um objeto sem nome com nomes de propriedades que são mapeados para nomes de coluna.|  
  
Se o cursor estiver no fim do conjunto de resultados (a última linha foi recuperada e o cursor avançou além do limite do conjunto de resultados) e se o cursor for somente de avanço (PDO::ATTR_CURSOR = PDO::CURSOR_FWDONLY), as chamadas de busca subsequentes falharão.  
  
Se o cursor for rolável (PDO::ATTR_CURSOR = PDO::CURSOR_SCROLL), a busca moverá o cursor dentro do limite do conjunto de resultados. A tabela a seguir contém a lista de possíveis $*cursor_orientation* valores.  
  
|$*cursor_orientation*|Description|  
|--------------------------|---------------|  
|PDO::FETCH_ORI_NEXT|Recupera a próxima linha. Esse é o padrão.|  
|PDO::FETCH_ORI_PRIOR|Recupera a linha anterior.|  
|PDO::FETCH_ORI_FIRST|Recupera a primeira linha.|  
|PDO::FETCH_ORI_LAST|Recupera a última linha.|  
|Fetch_ori_abs, *num*|Recupera a linha solicitada em $*cursor_offset* pelo número da linha.|  
|Fetch_ori_rel, *num*|Recupera a linha solicitada em $*cursor_offset* por posição relativa da posição atual.|  
  
Se o valor especificado para $*cursor_offset* ou $*cursor_orientation* resulta em uma posição fora do limite do conjunto de resultados, haverá falha na busca.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print( "\n---------- PDO::FETCH_CLASS -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg";  
      }  
  
      function __toString() {  
         return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
      }  
   }  
  
   $stmt->setFetchMode(PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
   while ( $row = $stmt->fetch(PDO::FETCH_CLASS)) {   
      print($row . "\n");   
   }  
  
   print( "\n---------- PDO::FETCH_INTO -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
   $c_obj = new cc( '' );  
  
   $stmt->setFetchMode(PDO::FETCH_INTO, $c_obj);  
   while ( $row = $stmt->fetch(PDO::FETCH_INTO)) {   
      echo "$c_obj\n";  
   }  
  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_ASSOC );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_NUM );  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_BOTH );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_LAZY );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_OBJ );  
   print $result->Name;  
   print( "\n \n" );  
  
   print( "\n---------- PDO::FETCH_BOUND -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->bindColumn('Name', $name);  
   $result = $stmt->fetch( PDO::FETCH_BOUND );  
   print $name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
