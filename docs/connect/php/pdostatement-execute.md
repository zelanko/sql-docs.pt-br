---
title: PDOStatement::execute | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 31e7465b2fca0d76f569afb83e3a7d8501fd6036
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936041"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Executa uma instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>parâmetros  
*$input*: (opcional) uma matriz associativa contendo os valores para os marcadores de parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
true se for bem-sucedido; caso contrário, false.  
  
## <a name="remarks"></a>Comentários  
Instruções executadas com PDOStatement::execute devem ser preparadas previamente com [PDO::prepare](../../connect/php/pdo-prepare.md). Consulte [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) para obter informações sobre como especificar a execução da instrução preparada ou direta.  
  
Todos os valores da matriz de parâmetros de entrada são tratados como valores PDO::PARAM_STR.  
  
Se a instrução preparada inclui marcadores de parâmetro, você deve chamar PDOStatement::bindParam para associar as variáveis PHP aos marcadores de parâmetro ou passar uma matriz de valores de parâmetro apenas de entrada.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
> [!NOTE]
> É recomendável usar cadeias de caracteres como entradas ao associar valores a uma [coluna decimal ou numérica](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) a fim de garantir a precisão e a exatidão, pois o PHP tem uma precisão limitada para [números de ponto flutuante](https://php.net/manual/en/language.types.float.php). O mesmo se aplica a colunas bigint, principalmente quando os valores estão fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
