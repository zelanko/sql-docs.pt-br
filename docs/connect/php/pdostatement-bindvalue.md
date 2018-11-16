---
title: PDOStatement::bindValue | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13bc4ece-420e-4887-8809-bf0705ddf126
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7ae069a5bb485f4b74a11b066f5871aba2f30ec
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606276"
---
# <a name="pdostatementbindvalue"></a>PDOStatement::bindValue
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Associa um valor a um espaço reservado nomeado ou de ponto de interrogação na instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::bindValue($parameter, $value[, $data_type]);  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*parameter*: um identificador do parâmetro (misto). Para uma instrução que usa espaços reservados nomeados, um nome de parâmetro (:name). Para uma instrução preparada usando a sintaxe de ponto de interrogação, esse será o índice de base 1 do parâmetro.
  
$*value*: o valor (misto) a ser associado ao parâmetro.  
  
$*data_type*: o tipo de dados (inteiro) opcional representado por uma constante PDO::PARAM_*. O padrão é PDO::PARAM_STR.  
  
## <a name="return-value"></a>Valor retornado  
TRUE se for bem-sucedido; caso contrário, FALSE.  
  
## <a name="remarks"></a>Remarks  
  
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
> É recomendável usar cadeias de caracteres como entradas ao associar os valores para um [coluna decimal ou numérica](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantir a precisão e a precisão, como PHP limitou a precisão para [números de ponto flutuante](https://php.net/manual/en/language.types.float.php). O mesmo se aplica a colunas bigint, especialmente quando os valores estão fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

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
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
