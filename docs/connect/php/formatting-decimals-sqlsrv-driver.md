---
title: Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV)
description: Saiba como usar as opções FormatDecimals e DecimalPlaces para formatar valores decimais ou monetários ao usar o Driver do Microsoft SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- formatting, decimal types, money values
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b111dd925a98c4f0380dfceb0a09ddffadb96592
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726813"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para preservar a precisão, [tipos decimais ou numéricos](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) são sempre buscados como cadeias de caracteres com precisão e escala exatas. Se qualquer valor for menor que 1, o zero à esquerda estará ausente. É o mesmo com campos money e smallmoney, pois são campos decimais com uma escala fixa igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adicionar zeros à esquerda se estiverem ausentes
Da versão 5.6.0 em diante, a opção `FormatDecimals` é adicionada aos níveis de conexão e de instrução do sqlsrv, o que permite ao usuário formatar cadeias de caracteres decimais. Essa opção espera um valor booliano (true ou false) e afeta apenas a formatação de valores decimais ou numéricos nos resultados buscados. Em outras palavras, a opção `FormatDecimals` não tem qualquer efeito sobre outras operações, como inserção ou atualização.

Por padrão, `FormatDecimals` é **false**. Se definido como true, os zeros à esquerda das cadeias de caracteres decimais serão adicionados para qualquer valor decimal menor que 1.

## <a name="configure-number-of-decimal-places"></a>Configurar o número de casas decimais
Com `FormatDecimals` ativado, outra opção, `DecimalPlaces`, permite que os usuários configurem o número de casas decimais ao exibir dados do tipo money e smallmoney. Ele aceita valores inteiros no intervalo de [0, 4] e o arredondamento pode ocorrer quando mostrado. No entanto, os dados do tipo money subjacentes permanecem os mesmos.

Ambas as opções podem ser definidas como nível de conexão ou de instrução e a configuração de instrução sempre substitui a configuração de conexão correspondente. Observe que a opção `DecimalPlaces` afeta **apenas** os dados do tipo money e `FormatDecimals` deve ser definida como true para que `DecimalPlaces` entre em vigor. Caso contrário, a formatação será desativada, independentemente da configuração `DecimalPlaces`.

> [!NOTE]
> Como os campos money ou smallmoney têm escala 4, configurar o valor de `DecimalPlaces` como um número negativo ou maior que 4 será ignorado. Não é recomendável usar nenhum dado do tipo money formatado como entrada para cálculos.

## <a name="example---a-simple-fetch"></a>Exemplo – uma busca simples
O exemplo a seguir mostra como usar as novas opções em uma busca simples.

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

## <a name="example---format-the-output-parameter"></a>Exemplo – formatar o parâmetro de saída
Se um campo decimal ou numérico for retornado como o [parâmetro de saída](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), o valor retornado será considerado uma cadeia de caracteres varchar normal. No entanto, se SQLSRV_SQLTYPE_DECIMAL ou SQLSRV_SQLTYPE_NUMERIC for especificado, você poderá definir `FormatDecimals` como true para garantir que não falte nenhum zero à esquerda no valor da cadeia de caracteres numérica. Para saber mais, leia [Como recuperar parâmetros de saída usando o driver SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

O exemplo a seguir mostra como formatar o parâmetro de saída de um procedimento armazenado que retorna um valor decimal (8,4).

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