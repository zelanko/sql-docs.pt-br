---
title: Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV) | Microsoft Docs
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
ms.openlocfilehash: 76b6d27acedcfe2ec462a764559237a1a2218f78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62669598"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para preservar a exatidão, [tipos decimais ou numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) sempre são buscados como cadeias de caracteres com as precisões exatas e escalas. Se nenhum valor for menor que 1, o zero à esquerda está ausente. É o mesmo com campos money e smallmoney conforme eles são campos decimais com uma escala fixa igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adicionar zeros à esquerda se ausente
Começando com a versão 5.6.0, a opção `FormatDecimals` é adicionado aos níveis de conexão e instrução sqlsrv, que permite ao usuário formatar cadeias de caracteres decimais. Essa opção espera um valor booliano (verdadeiro ou falso) e só afeta a formatação de valores numéricos ou decimais nos resultados da buscados. Em outras palavras, o `FormatDecimals` opção não tem nenhum efeito nas outras operações, como inserção ou atualização.

Por padrão, `FormatDecimals` é **false**. Se definido como true, os zeros à esquerda para cadeias de caracteres decimais será adicionado para qualquer valor decimal menor que 1.

## <a name="configure-number-of-decimal-places"></a>Configurar o número de casas decimais
Com o `FormatDecimals` ativado, outra opção, `DecimalPlaces`, permite que os usuários configurem o número de casas decimais, ao exibir dados money e smallmoney. Ele aceita valores inteiros no intervalo de [0, 4], e o arredondamento pode ocorrer quando mostrada. No entanto, os dados subjacentes do dinheiro permanecem os mesmos.

Ambas as opções podem ser definidas para conexão ou o nível de instrução e a instrução configuração sempre substitui a configuração de conexão correspondente. Observe que o `DecimalPlaces` opção **apenas** afeta os dados de dinheiro, e `FormatDecimals` deve ser definido como verdadeiro para `DecimalPlaces` entrem em vigor. Caso contrário, formatação está desativado independentemente de `DecimalPlaces` configuração.

> [!NOTE]
> Como dinheiro ou smallmoney campos têm uma escala de 4, definindo `DecimalPlaces` valor para qualquer número negativo ou qualquer valor maior do que 4 serão ignoradas. Não é recomendável usar todos os dados formatados de dinheiro como entradas para qualquer cálculo.

## <a name="example---a-simple-fetch"></a>Exemplo – uma busca simple
O exemplo a seguir mostra como usar as novas opções em uma busca simple.

```php
<?php
$username = 'myusername';
$password = 'mypasword';
$tableName = 'mytable';

$connectionInfo = array("UID" => $username, "PWD" => $password, "Database" => "myDB", "FormatDecimals" => true);  
$server = "myServer";  // IP address also works
$conn = sqlsrv_connect( $server, $connectionInfo);  

$numDigits = 2;
$query = "SELECT money1 FROM $tableName";
$options = array("DecimalPlaces" => $numDigits);
$stmt = sqlsrv_prepare($conn, $query, array(), $options);
sqlsrv_execute($stmt);

if (sqlsrv_fetch($stmt)) {
    $field = sqlsrv_get_field($stmt, 0);  
    echo $field;   // expect a numeric value string with 2 decimal places
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="example---format-the-output-parameter"></a>Exemplo - formato de parâmetro de saída
Se um campo numérico ou decimal é retornado como o [parâmetro de saída](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), o valor retornado será ser considerado como uma cadeia de caracteres regulares varchar. No entanto, se SQLSRV_SQLTYPE_DECIMAL ou SQLSRV_SQLTYPE_NUMERIC for especificado, você pode definir `FormatDecimals` como true para garantir que não há nenhum zero à esquerda para o valor de cadeia de caracteres numérica ausente. Para saber mais, leia [Como recuperar parâmetros de saída usando o driver SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

O exemplo a seguir mostra como formatar o parâmetro de saída de um procedimento armazenado que retorna um valor de decimal(8,4).

```php
$outString = '';
$outSql = '{CALL myStoredProc(?)}';
$stmt = sqlsrv_prepare($conn, 
                       $outSql, 
                       array(array(&$outString, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_DECIMAL(8, 4))),
                       array('FormatDecimals' => true));

if (sqlsrv_execute($stmt)) {
    echo $outString;  // expect a numeric value string with no missing leading zero
}
```

## <a name="see-also"></a>Consulte Também
[Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md)

[Recuperando dados](../../connect/php/retrieving-data.md)
