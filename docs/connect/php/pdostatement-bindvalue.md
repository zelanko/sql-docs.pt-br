---
title: PDOStatement::bindValue | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13bc4ece-420e-4887-8809-bf0705ddf126
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 910b5326d910f57056ac885a91762496a96d7a0a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="pdostatementbindvalue"></a>PDOStatement::bindValue
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Associa um valor a um espaço reservado nomeado ou de ponto de interrogação na instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::bindValue($parameter, $value[, $data_type]);  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*parâmetro*: um identificador do parâmetro (misto). Para uma instrução que usa espaços reservados nomeados, use um nome de parâmetro (: name). Para uma instrução preparada usando a sintaxe de ponto de interrogação, é o índice baseado em 1 do parâmetro.
  
$*valor*: O valor (misto) para associar ao parâmetro.  
  
$*data_type*: O tipo de dados opcional (inteiro) representado por uma constante PDO::PARAM_ *. O padrão é PDO::PARAM_STR.  
  
## <a name="return-value"></a>Valor de retorno  
TRUE se for bem-sucedido; caso contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra que depois que o valor de $contact é associado, a alteração do valor não altera o valor passado na consulta.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindValue(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindValue(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```

> [!NOTE]
> É recomendável usar cadeias de caracteres como entradas ao associar valores para um [coluna decimal ou numeric](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantir a precisão e a precisão, como PHP limitou a precisão para [números de ponto flutuante](http://php.net/manual/en/language.types.float.php).

## <a name="example"></a>Exemplo  
Este exemplo de código mostra como associar um valor decimal como um parâmetro de entrada.  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindValue(1, $input, PDO::PARAM_STR);
$stmt->execute();
```
  
## <a name="see-also"></a>Consulte também  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
