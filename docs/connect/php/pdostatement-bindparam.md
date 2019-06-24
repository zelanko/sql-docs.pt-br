---
title: PDOStatement::bindParam | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65212058-2632-47a4-ba7d-2206883abf09
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d8186b87e5dde50b07aa69e4dde870d8474265bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795587"
---
# <a name="pdostatementbindparam"></a>PDOStatement::bindParam
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Associa um parâmetro a um espaço reservado nomeado ou de ponto de interrogação na instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::bindParam($parameter, &$variable[, $data_type[, $length[, $driver_options]]]);  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*parameter*: um identificador do parâmetro (misto). Para uma instrução que usa espaços reservados nomeados, um nome de parâmetro (:name). Para uma instrução preparada usando a sintaxe de ponto de interrogação, esse será o índice de base 1 do parâmetro.  
  
&$*variable*: o nome (misto) da variável do PHP a ser associada ao parâmetro da instrução SQL.  
  
$*data_type*: uma constante PDO::PARAM_* (inteiro) opcional. O padrão é PDO::PARAM_STR.  
  
$*length*: um comprimento opcional (inteiro) do tipo de dados. Você pode especificar PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE para indicar o tamanho padrão ao usar PDO::PARAM_INT ou PDO::PARAM_BOOL in $*data_type*.  
  
$*driver_options*: as opções específicas do driver (mistas) opcionais. Por exemplo, você poderia especificar PDO::SQLSRV_ENCODING_UTF8 para associar a coluna a uma variável como uma cadeia de caracteres codificada em UTF-8.  
  
## <a name="return-value"></a>Valor retornado  
TRUE se for bem-sucedido; caso contrário, FALSE.  
  
## <a name="remarks"></a>Remarks  
Ao associar dados nulos a colunas do servidor do tipo varbinary, binary ou varbinary(max), você deve especificar a codificação binária (PDO::SQLSRV_ENCODING_BINARY) usando $*driver_options*. Para obter mais informações sobre a codificação de constantes, veja [Constantes](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="example"></a>Exemplo  
Este exemplo de código mostra que, depois que $contact é associado ao parâmetro, a alteração do valor não altera o valor passado na consulta.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindParam(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindParam(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```  
  
## <a name="example"></a>Exemplo  
Este exemplo de código mostra como acessar um parâmetro de saída.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$input1 = 'bb';  
  
$stmt = $conn->prepare("select ? = count(*) from Sys.tables");  
$stmt->bindParam(1, $input1, PDO::PARAM_STR, 10);  
$stmt->execute();  
echo $input1;  
?>  
```  
  
> [!NOTE]
> Ao associar um parâmetro de saída para um tipo bigint, se o valor pode acabar fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), usando PDO:: param_int com PDO:: sqlsrv_param_out_default_size pode resultar em uma exceção de "valor fora do intervalo". Portanto, use o PDO:: param_str padrão em vez disso e forneça o tamanho da cadeia de caracteres resultante, que é, no máximo, 21. É o número máximo de dígitos, incluindo o sinal de negativo, de qualquer valor bigint. 

## <a name="example"></a>Exemplo  
Este exemplo de código mostra como usar um parâmetro de entrada/saída.  
  
```  
<?php  
   $database = "AdventureWorks";  
   $server = "(local)";  
   $dbh = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
   $dbh->query("IF OBJECT_ID('dbo.sp_ReverseString', 'P') IS NOT NULL DROP PROCEDURE dbo.sp_ReverseString");  
   $dbh->query("CREATE PROCEDURE dbo.sp_ReverseString @String as VARCHAR(2048) OUTPUT as SELECT @String = REVERSE(@String)");  
   $stmt = $dbh->prepare("EXEC dbo.sp_ReverseString ?");  
   $string = "123456789";  
   $stmt->bindParam(1, $string, PDO::PARAM_STR | PDO::PARAM_INPUT_OUTPUT, 2048);  
   $stmt->execute();  
   print $string;   // Expect 987654321  
?>  
```  

> [!NOTE]
> É recomendável usar cadeias de caracteres como entradas ao associar valores a uma [coluna decimal ou numérica](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) a fim de garantir a precisão e a exatidão, pois o PHP tem uma precisão limitada para [números de ponto flutuante](https://php.net/manual/en/language.types.float.php). O mesmo se aplica a colunas bigint, principalmente quando os valores estão fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

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
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```


## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
