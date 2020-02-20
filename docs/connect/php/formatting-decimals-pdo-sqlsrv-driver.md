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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68265151"
---
# <a name="formatting-decimal-strings-and-money-values-pdo_sqlsrv-driver"></a>Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para preservar a precisão, [tipos decimais ou numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) são sempre buscados como cadeias de caracteres com precisão e escala exatas. Se qualquer valor for menor que 1, o zero à esquerda estará ausente. É o mesmo com campos money e smallmoney, pois são campos decimais com uma escala fixa igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adicionar zeros à esquerda se estiverem ausentes
Da versão 5.6.0 em diante, o atributo de conexão ou instrução `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` permite que o usuário formate cadeias de caracteres decimais. Esse atributo espera um valor booliano (true ou false) e afeta apenas a formatação de valores decimais ou numéricos nos resultados buscados. Em outras palavras, esse atributo não tem qualquer efeito sobre outras operações, como inserção ou atualização.

Por padrão, `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` é **false**. Se definido como true, os zeros à esquerda das cadeias de caracteres decimais serão adicionados para qualquer valor decimal menor que 1.

## <a name="configure-number-of-decimal-places"></a>Configurar o número de casas decimais
Com `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` ativado, outro atributo de conexão ou instrução, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, permite que os usuários configurem o número de casas decimais ao exibir dados do tipo money e smallmoney. Ele aceita valores inteiros no intervalo de [0, 4] e o arredondamento pode ocorrer quando mostrado. No entanto, os dados do tipo money subjacentes permanecem os mesmos.

Os atributos de instrução sempre substituem as configurações de conexão correspondentes. Observe que a opção `PDO::SQLSRV_ATTR_DECIMAL_PLACES` afeta **apenas** os dados do tipo money e `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` deve ser definida como true. Caso contrário, a formatação será desativada, independentemente da configuração `PDO::SQLSRV_ATTR_DECIMAL_PLACES`.

> [!NOTE]
> Como os campos money ou smallmoney têm escala 4, configurar `PDO::SQLSRV_ATTR_DECIMAL_PLACES` como um número negativo ou maior que 4 será ignorado. Não é recomendável usar nenhum dado do tipo money formatado como entrada para cálculos.

### <a name="to-set-the-connection-attributes"></a>Para definir os atributos de conexão

-   Definir atributos no ponto de conexão:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Definir atributos após a conexão:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Exemplo – formatar dados do tipo money
O seguinte exemplo mostra como buscar dados do tipo money usando [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>Exemplo – substituir os atributos de conexão
O seguinte exemplo mostra como substituir os atributos de conexão:

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
