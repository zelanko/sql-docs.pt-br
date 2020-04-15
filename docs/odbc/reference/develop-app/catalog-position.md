---
title: Posição do Catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0305d978dc4ecd21892a0be3916fa5072b7be95a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303377"
---
# <a name="catalog-position"></a>Posição de catálogo
A posição de um nome de catálogo em um identificador e como ele é separado do resto do identificador varia de fonte de dados para fonte de dados. Por exemplo, em uma fonte de dados Xbase, o nome do catálogo é um diretório e, no Microsoft® Windows®,\\é separado do nome da tabela (que é um nome de arquivo) por uma barra invertida (). A ilustração a seguir demonstra esta condição.  
  
 ![Posição de catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 Em uma fonte de dados do SQL Server, o catálogo é um banco de dados e é separado do esquema e nomes de tabela por um período (.).  
  
 ![Postagem do catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Em uma fonte de dados Oracle, o catálogo também é o banco de dados, mas segue o nome da tabela e é separado do esquema e nomes de tabela por um sinal at (@).  
  
 ![Posição de catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar o separador do catálogo e a localização do nome do catálogo, um aplicativo chama **sqlGetInfo** com as opções SQL_CATALOG_NAME_SEPARATOR e SQL_CATALOG_LOCATION. As aplicações interoperáveis devem construir identificadores de acordo com esses valores.  
  
 Ao citar identificadores que contenham mais de uma parte, os aplicativos devem ter o cuidado de citar cada parte separadamente e não citar o caractere que separa os identificadores. Por exemplo, a seguinte declaração para selecionar todas as linhas e colunas de uma tabela Xbase cita os nomes de catálogo (\XBASE\SALES\CORP) e tabela (Parts.dbf), mas não o separador de catálogo ():\\  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 A seguinte declaração para selecionar todas as linhas e colunas de uma tabela Oracle cita os nomes do catálogo (Vendas), esquema (Corporativo) e tabela (Partes), mas não os separadores de catálogo (@) ou esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obter informações sobre a citação de identificadores, consulte a próxima seção, [Identificadores citados](../../../odbc/reference/develop-app/quoted-identifiers.md).
