---
title: "Posição de catálogo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dd67618a952e189a1ce7b3596f68dddd16977ae3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-position"></a>Posição de catálogo
A posição de um nome de catálogo em um identificador e como ele é separado do resto do identificador varia de fonte de dados para a fonte de dados. Por exemplo, em uma fonte de dados Xbase, o nome do catálogo é um diretório e, no Microsoft® Windows®, é separado do nome de tabela (que é um nome de arquivo) por uma barra invertida (\\). A ilustração a seguir demonstra essa condição.  
  
 ![Posição de catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 Em uma fonte de dados do SQL Server, o catálogo é um banco de dados e é separado dos nomes de esquema e da tabela por um ponto (.).  
  
 ![Posição de catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Em uma fonte de dados Oracle, o catálogo também é o banco de dados, mas segue o nome da tabela e é separado dos nomes de esquema e da tabela por um sinal de arroba (@).  
  
 ![Posição de catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar o separador de catálogo e o local do nome do catálogo, um aplicativo chama **SQLGetInfo** com as opções SQL_CATALOG_NAME_SEPARATOR e SQL_CATALOG_LOCATION. Aplicativos interoperáveis devem construir identificadores de acordo com esses valores.  
  
 Quando delimitar identificadores que contêm mais de uma parte, aplicativos devem ter cuidadosos para cada parte da cotação separadamente e não o caractere que separa os identificadores da cotação. Por exemplo, a instrução a seguir para selecionar todas as linhas e colunas de uma tabela Xbase aspas o catálogo (\XBASE\SALES\CORP) e nomes de tabela (Parts.dbf), mas não o separador de catálogo (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 A instrução a seguir para selecionar todas as linhas e colunas de uma tabela de Oracle aspas o catálogo (vendas), o esquema (corporativo) e nomes de tabela (partes), mas não o catálogo (@) ou separadores de esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obter informações sobre delimitar identificadores, consulte a próxima seção, [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).

