---
title: Tipos de cursor (Driver PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49ea6a6e-78d4-40f8-85eb-180b527f0537
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ced7dd299104bfc37c6437123ca1da1cfd052f8e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cursor-types-pdosqlsrv-driver"></a>Tipos de cursor (Driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O driver PDO_SQLSRV permite criar conjuntos de resultados roláveis com um dos vários cursores.  
  
Para obter informações sobre como especificar um cursor usando o driver PDO_SQLSRV e para obter exemplos de código, consulte [PDO](../../connect/php/pdo-prepare.md).  
  
## <a name="pdosqlsrv-and-server-side-cursors"></a>PDO_SQLSRV e cursores do lado do servidor  
Antes da versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], o driver PDO_SQLSRV permitido criar um conjunto de resultados com um cursor de somente avanço ou estático do lado do servidor. Começando na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], o conjunto de chaves e cursores dinâmicos também estão disponíveis.  
  
Você pode indicar o tipo de cursor do lado do servidor usando o PDO:: Prepare ou pdostatement:: setAttribute para selecionar o tipo de cursor:  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_FWDONLY  
  
-   PDO:: ATTR_CURSOR = &GT; PDO:: CURSOR_SCROLL  
  
Você pode solicitar um cursor keyset ou dynamic especificando PDO:: attr_cursor = > PDO:: cursor_scroll e, em seguida, passe o valor apropriado para PDO:: sqlsrv_attr_cursor_scroll_type. Os valores possíveis que você pode passar para PDO:: sqlsrv_attr_cursor_scroll_type são:  
  
-   PDO::SQLSRV_CURSOR_BUFFERED  
  
-   PDO::SQLSRV_CURSOR_DYNAMIC  
  
-   PDO::SQLSRV_CURSOR_KEYSET_DRIVEN  
  
-   PDO::SQLSRV_CURSOR_STATIC  
  
## <a name="pdosqlsrv-and-client-side-cursors"></a>PDO_SQLSRV e cursores do lado do cliente  
Cursores do lado do cliente foram adicionados na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que permite que você armazene um todo conjunto de resultados na memória. Uma vantagem é que a contagem de linhas está disponível depois que uma consulta é executada.  
  
Cursores do lado do cliente devem ser usados para conjuntos de resultados de pequeno a médio porte. Conjuntos de resultados grandes devem usar cursores do lado do servidor.  
  
Uma consulta retornará false se o buffer não é grande o suficiente para manter um todo conjunto de resultados ao usar um cursor do lado do cliente. Você pode aumentar o tamanho do buffer até o limite de memória do PHP.  
  
Você pode configurar o tamanho do buffer que contém o conjunto de resultados com o atributo PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE do [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) ou [pdostatement:: setAttribute](../../connect/php/pdostatement-setattribute.md). Você também pode definir o tamanho máximo do buffer no arquivo php.ini com pdo_sqlsrv.client_buffer_max_kb_size (por exemplo, pdo_sqlsrv.client_buffer_max_kb_size = 1024).  
  
Indicar que você quer um cursor do lado do cliente usando o PDO:: Prepare ou pdostatement:: setAttribute e selecione o PDO:: attr_cursor = > PDO:: cursor_scroll tipo de cursor.  Você então especificar PDO:: sqlsrv_attr_cursor_scroll_type = > PDO::SQLSRV_CURSOR_BUFFERED.  
  
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
  
## <a name="see-also"></a>Consulte também  
[Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
