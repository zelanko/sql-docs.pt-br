---
title: PDOStatement::fetchObject | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 71ad1932-cab3-4c29-8950-f5e82547d3b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c65d059d786d33f324ba254f23216269c0ca0f80
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604387"
---
# <a name="pdostatementfetchobject"></a>PDOStatement::fetchObject
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera a próxima linha como um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDOStatement::fetchObject([ $class_name[,$ctor_args ]] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*class_name*: uma cadeia de caracteres opcional que especifica o nome da classe a ser criada. O padrão é stdClass.  
  
$*ctor_args*: uma matriz opcional com argumentos para um construtor de classe personalizada.  
  
## <a name="return-value"></a>Valor retornado  
Em caso de sucesso, retorna um objeto com uma instância da classe. Propriedades mapeiam para colunas. Retorna falso em caso de falha.  
  
## <a name="remarks"></a>Remarks  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchObject();  
   print $result->Name;  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
