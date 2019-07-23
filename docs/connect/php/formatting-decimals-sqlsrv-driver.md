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
manager: v-mabarw
ms.openlocfilehash: 4a5ac641a98077c09bb38a5fc8fbd3fb1a4bf73d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265141"
---
# <a name="formatting-decimal-strings-and-money-values-sqlsrv-driver"></a>Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para preservar a precisão, os [tipos decimais ou numéricos](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) são sempre buscados como cadeias de caracteres com precisão e escalações exatas. Se qualquer valor for menor que 1, o zero à esquerda estará ausente. É o mesmo com campos Money e smallmoney, pois são campos decimais com uma escala fixa igual a 4.

## <a name="add-leading-zeroes-if-missing"></a>Adicionar zeros à esquerda se estiverem ausentes
A partir da versão 5.6.0, a `FormatDecimals` opção é adicionada aos níveis de conexão sqlsrv e de instrução, o que permite ao usuário Formatar cadeias de caracteres decimais. Essa opção espera um valor booliano (true ou false) e afeta apenas a formatação de valores decimais ou numéricos nos resultados obtidos. Em outras palavras, a `FormatDecimals` opção não tem nenhum efeito sobre outras operações, como inserção ou atualização.

Por padrão, `FormatDecimals` é **false**. Se definido como true, os zeros à esquerda para cadeias de caracteres decimais serão adicionados para qualquer valor decimal menor que 1.

## <a name="configure-number-of-decimal-places"></a>Configurar número de casas decimais
Com `FormatDecimals` ativado, outra opção, `DecimalPlaces`, permite que os usuários configurem o número de casas decimais ao exibir dados Money e smallmoney. Ele aceita valores inteiros no intervalo de [0, 4] e o arredondamento pode ocorrer quando mostrado. No entanto, os dados do Money subjacentes permanecem os mesmos.

Ambas as opções podem ser definidas como nível de conexão ou de instrução, e a configuração da instrução sempre substitui a configuração de conexão correspondente. Observe que a `DecimalPlaces` opção afeta **apenas** os dados do Money `FormatDecimals` e deve ser definida como true `DecimalPlaces` para entrar em vigor. Caso contrário, a formatação será desativada independentemente da `DecimalPlaces` configuração.

> [!NOTE]
> Como os campos Money ou smallmoney têm escala 4, `DecimalPlaces` definir valor como qualquer número negativo ou qualquer valor maior que 4 será ignorado. Não é recomendável usar nenhum dado de dinheiro formatado como entradas para qualquer cálculo.

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
Se um campo decimal ou numérico for retornado como o [parâmetro de saída](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md), o valor retornado será considerado uma cadeia de caracteres varchar regular. No entanto, se SQLSRV_SQLTYPE_DECIMAL ou SQLSRV_SQLTYPE_NUMERIC for especificado, você poderá `FormatDecimals` definir como true para garantir que não haja nenhum zero à esquerda para o valor numérico da cadeia de caracteres. Para saber mais, leia [Como recuperar parâmetros de saída usando o driver SQLSRV](../..//connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).

O exemplo a seguir mostra como formatar o parâmetro de saída de um procedimento armazenado que retorna um valor decimal (8, 4).

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
