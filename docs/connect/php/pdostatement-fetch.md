---
title: PDOStatement::fetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4368e362-5bda-4da1-8462-33714683c39f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: afd2f2fc098e23685dca1b913e010dced40cece9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799178"
---
# <a name="pdostatementfetch"></a>PDOStatement::fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera uma linha de um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDOStatement::fetch ([ $fetch_style[, $cursor_orientation[, $cursor_offset]]] );  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*fetch_style*: um símbolo (inteiro) opcional especificando o formato dos dados da linha. Consulte a seção Comentários para obter a lista de valores possíveis para $*fetch_style*. O padrão é PDO::FETCH_BOTH. $*fetch_style* no método de busca substituirá o $*fetch_style* especificado no método PDO::query.  
  
$*cursor_orientation*: um símbolo (inteiro) opcional que indica a linha a ser recuperada quando a instrução prepare especifica `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`. Consulte a seção Comentários para obter a lista de valores possíveis para $*cursor_orientation*. Consulte [PDO::prepare](../../connect/php/pdo-prepare.md) para obter um exemplo usando um cursor rolável.  
  
$*cursor_offset*: um símbolo (inteiro) opcional que especifica a linha a ser buscada quando$*cursor_orientation* é PDO::FETCH_ORI_ABS ou PDO::FETCH_ORI_REL e PDO::ATTR_CURSOR é PDO::CURSOR_SCROLL.  
  
## <a name="return-value"></a>Valor retornado  
Um valor misto que retorna uma linha ou false.  
  
## <a name="remarks"></a>Remarks  
O cursor é avançado automaticamente quando a busca é chamada. A tabela a seguir contém a lista de possíveis valores de $*fetch_style*.  
  
|$*fetch_style*|Descrição|  
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
  
Se o cursor for rolável (PDO::ATTR_CURSOR = PDO::CURSOR_SCROLL), a busca moverá o cursor dentro do limite do conjunto de resultados. A tabela a seguir contém a lista de possíveis valores de $*cursor_orientation*.  
  
|$*cursor_orientation*|Descrição|  
|--------------------------|---------------|  
|PDO::FETCH_ORI_NEXT|Recupera a próxima linha. Esse é o padrão.|  
|PDO::FETCH_ORI_PRIOR|Recupera a linha anterior.|  
|PDO::FETCH_ORI_FIRST|Recupera a primeira linha.|  
|PDO::FETCH_ORI_LAST|Recupera a última linha.|  
|PDO::FETCH_ORI_ABS, *num*|Recupera a linha solicitada em $*cursor_offset* pelo número da linha.|  
|PDO::FETCH_ORI_REL, *num*|Recupera a linha solicitada em $*cursor_offset* por posição relativa com base na posição atual.|  
  
Se o valor especificado para $*cursor_offset* ou $*cursor_orientation* resultar em uma posição fora do limite do conjunto de resultados, haverá falha na busca.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
