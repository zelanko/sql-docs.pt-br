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
manager: mbarwin
ms.openlocfilehash: 35626c192c3d74ad0201cee3c5e97adbce92a3aa
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676510"
---
# <a name="formatting-decimal-strings-and-money-values-pdosqlsrv-driver"></a>Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para preservar a exatidão, [tipos decimais ou numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) sempre são buscados como cadeias de caracteres com as precisões exatas e escalas. Se nenhum valor for menor que 1, o zero à esquerda está ausente. É o mesmo com campos money e smallmoney conforme eles são campos decimais com uma escala fixa igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adicionar zeros à esquerda se ausente
Começando com a versão 5.6.0, a conexão ou o atributo de instrução `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` permite ao usuário formatar cadeias de caracteres decimais. Esse atributo espera um valor booliano (verdadeiro ou falso) e só afeta a formatação dos valores numéricos ou decimais nos resultados da buscados. Em outras palavras, esse atributo não tem efeito em outras operações, como inserção ou atualização.

Por padrão, `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` é **false**. Se definido como true, os zeros à esquerda para cadeias de caracteres decimais será adicionado para qualquer valor decimal menor que 1.

## <a name="configure-number-of-decimal-places"></a>Configurar o número de casas decimais
Com o `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` ativado, outro atributo de conexão ou instrução, `PDO::SQLSRV_ATTR_DECIMAL_PLACES`, permite que os usuários configurem o número de casas decimais, ao exibir dados money e smallmoney. Ele aceita valores inteiros no intervalo de [0, 4], e o arredondamento pode ocorrer quando mostrada. No entanto, os dados subjacentes do dinheiro permanecem os mesmos.

Os atributos de instrução sempre substituem as configurações de conexão correspondentes. Observe que o `PDO::SQLSRV_ATTR_DECIMAL_PLACES` opção **apenas** afeta os dados de dinheiro e `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` deve ser definida como true. Caso contrário, formatação está desativado independentemente de `PDO::SQLSRV_ATTR_DECIMAL_PLACES` configuração.

> [!NOTE]
> Como dinheiro ou smallmoney campos têm uma escala de 4, definindo `PDO::SQLSRV_ATTR_DECIMAL_PLACES` para qualquer número negativo ou qualquer valor maior do que 4 serão ignoradas. Não é recomendável usar todos os dados formatados de dinheiro como entradas para qualquer cálculo.

### <a name="to-set-the-connection-attributes"></a>Para definir os atributos de conexão

-   Definir atributos no ponto de conexão:

    ```php
    $attrs = array(PDO::SQLSRV_ATTR_FORMAT_DECIMALS => true,
                   PDO::SQLSRV_ATTR_DECIMAL_PLACES => 2);

    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password, $attrs);
    ```

-   Definir atributos de conexão de postagem:

    ```php
    $conn = new PDO("sqlsrv:Server = myServer; Database = myDB", $username, $password);
    $conn->setAttribute(PDO::SQLSRV_ATTR_FORMAT_DECIMALS, true);
    $conn->setAttribute(PDO::SQLSRV_ATTR_DECIMAL_PLACES, 2);
    ```

## <a name="example---format-money-data"></a>Exemplo – dados de formato de dinheiro
O exemplo a seguir mostra como buscar dados de dinheiro usando [pdostatement:: Bindcolumn](../../connect/php/pdostatement-bindcolumn.md):

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

## <a name="example---override-connection-attributes"></a>Exemplo – atributos de conexão de substituição
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
