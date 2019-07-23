---
title: Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 76c314159faf15e63bf77b17a8a45abf217b205c
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265151"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para preservar a precisão, os [tipos decimais ou numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) são sempre buscados como cadeias de caracteres com precisão e escalações exatas. Se qualquer valor for menor que 1, o zero à esquerda estará ausente. É o mesmo com campos Money e smallmoney, pois são campos decimais com uma escala fixa igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adicionar zeros à esquerda se estiverem ausentes
A partir da versão 5.6.0, o atributo `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` Connection ou Statement permite que o usuário formate cadeias de caracteres decimais. Esse atributo espera um valor booliano (true ou false) e afeta apenas a formatação dos valores decimais ou numéricos nos resultados obtidos. Em outras palavras, esse atributo não tem nenhum efeito sobre outras operações, como inserção ou atualização.

Por padrão, `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` é **false**. Se definido como true, os zeros à esquerda para cadeias de caracteres decimais serão adicionados para qualquer valor decimal menor que 1.

## <a name="configure-number-of-decimal-places"></a>Configurar número de casas decimais
Com `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` o ativado, outro atributo de conexão ou de `PDO::SQLSRV_ATTR_DECIMAL_PLACES`instrução,, permite que os usuários configurem o número de casas decimais ao exibir dados de Money e smallmoney. Ele aceita valores inteiros no intervalo de [0, 4] e o arredondamento pode ocorrer quando mostrado. No entanto, os dados do Money subjacentes permanecem os mesmos.

Os atributos da instrução sempre substituem as configurações de conexão correspondentes. Observe que a `PDO::SQLSRV_ATTR_DECIMAL_PLACES` opção afeta **apenas** os dados do Money `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` e deve ser definida como true. Caso contrário, a formatação será desativada independentemente da `PDO::SQLSRV_ATTR_DECIMAL_PLACES` configuração.

> [!NOTE]
> Como os campos Money ou smallmoney têm escala 4, `PDO::SQLSRV_ATTR_DECIMAL_PLACES` a configuração para qualquer número negativo ou qualquer valor maior que 4 será ignorada. Não é recomendável usar nenhum dado de dinheiro formatado como entradas para qualquer cálculo.

### <a name="to-set-the-connection-attributes"></a>Para definir os atributos de conexão

-   Definir atributos no ponto de conexão:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Definir atributos pós-conexão:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Exemplo-formatar dados do Money
O exemplo a seguir mostra como buscar dados do Money usando [PDOStatement:: bindColumn](../../connect/php/pdostatement-bindcolumn.md):

```php
<?php
$database = "myDB";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);

$numDigits = 3;
$query = "SELECT smallmoney1 FROM aTable";
$options = array(PDO::SQLSRV_ATTR_DECIMAL_PLACES => $numDigits);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);
echo $field;    // expect a number string with 3 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="example---override-connection-attributes"></a>Exemplo – substituir atributos de conexão
O exemplo a seguir mostra como substituir os atributos de conexão:

```php
<?php
$database = 'myDatabase';
$server = 'myServer';
$username = 'myuser';
$password = 'mypassword'

$conn = new PDO("sqlsrv:server=$server; Database = $database", $username, $password);
$conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
$conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);

$query = 'SELECT smallmoney1 FROM testTable1';
$options = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();

$stmt->bindColumn('smallmoney1', $field);
$result = $stmt->fetch(PDO::FETCH_BOUND);  
echo $field;   // expect a number string showing the original scale -- 4 decimal places

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>Consulte Também
[Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV)](../../connect/php/formatting-decimals-sqlsrv-driver.md)

[Recuperando dados](../../connect/php/retrieving-data.md)
