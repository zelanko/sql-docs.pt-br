---
title: Tipos de cursor (Driver PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c33d1dffef3e2a7cfd6b981f8bfb0087969e88b7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928059"
---
# <a name="cursor-types-pdo_sqlsrv-driver"></a>Tipos de cursor (Driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O driver PDO_SQLSRV permite que você crie conjuntos de resultados roláveis com um dos vários cursores.

Para obter informações sobre como especificar um cursor usando o driver PDO_SQLSRV e para obter exemplos do código, confira [PDO::prepare](../../connect/php/pdo-prepare.md).

## <a name="pdo_sqlsrv-and-server-side-cursors"></a>PDO_SQLSRV e cursores do lado do servidor
Antes da versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], o driver PDO_SQLSRV permitia que você criasse um conjunto de resultados com um cursor estático ou somente de avanço do lado do servidor. Começando na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], também estão disponíveis os cursores dinâmicos e de conjunto de chaves.

Você pode indicar o tipo de cursor do lado do servidor usando [PDO::prepare](../../connect/php/pdo-prepare.md) para selecionar um dos seguintes tipos de cursores:

-   `PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY`

-   `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`

Você pode solicitar um cursor estático, dinâmico ou conjunto de chaves especificando `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` e, em seguida, passando o valor apropriado para `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`. Os valores possíveis que você pode passar para `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` para cursores do lado do servidor são:

-   `PDO::SQLSRV_CURSOR_DYNAMIC`

-   `PDO::SQLSRV_CURSOR_STATIC`

-   `PDO::SQLSRV_CURSOR_KEYSET`

## <a name="pdo_sqlsrv-and-client-side-cursors"></a>PDO_SQLSRV e cursores do lado do cliente
Os cursores do lado do cliente foram adicionados na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] e permitem armazenar em cache na memória todo um conjunto de resultados. Uma vantagem é que a contagem de linhas está disponível depois que uma consulta é executada.

Os cursores do lado do cliente devem ser usados para conjuntos de resultados pequeno a médio porte. Os conjuntos de resultados de grande porte devem usar cursores do lado do servidor.

Uma consulta retornará false se o buffer não for grande o suficiente para manter todo o conjunto de resultados ao usar um cursor do lado do cliente. Você pode aumentar o tamanho do buffer até o limite de memória do PHP.

É possível configurar o tamanho do buffer que contém o conjunto de resultados com o atributo `PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE` de [PDO::setAttribute](../../connect/php/pdo-setattribute.md) ou [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md). Você também pode definir o tamanho máximo do buffer no arquivo php.ini com pdo_sqlsrv.client_buffer_max_kb_size (por exemplo, pdo_sqlsrv.client_buffer_max_kb_size = 1024).

É possível solicitar um cursor do lado do cliente usando [PDO::prepare](../../connect/php/pdo-prepare.md), especificando o tipo de cursor `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` e, em seguida, especificando `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED`.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como especificar um cursor em buffer.
```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_BUFFERED));
$stmt->execute();
print $stmt->rowCount();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

## <a name="see-also"></a>Consulte Também
[Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)

