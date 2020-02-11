---
title: Posição do catálogo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3d7c320521a9948c7968f4f7f5d42fd715f6c03d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062678"
---
# <a name="catalog-position"></a>Posição de catálogo
A posição de um nome de catálogo em um identificador e como ele é separado do restante do identificador varia de fonte de dados para fonte de dados. Por exemplo, em uma fonte de dados Xbase, o nome do catálogo é um diretório e, no Microsoft® Windows®, é separado do nome da tabela (que é um nome de arquivo) por uma\\barra invertida (). A ilustração a seguir demonstra essa condição.  
  
 ![Posição de catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 Em uma fonte de dados SQL Server, o catálogo é um banco de dado e é separado dos nomes de esquema e tabela por um ponto (.).  
  
 ![Postagem de catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Em uma fonte de dados Oracle, o catálogo também é o banco de dado, mas segue o nome da tabela e é separado dos nomes de esquema e tabela por um sinal de arroba (@).  
  
 ![Posição de catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar o separador de catálogo e o local do nome do catálogo, um aplicativo chama **SQLGetInfo** com as opções SQL_CATALOG_NAME_SEPARATOR e SQL_CATALOG_LOCATION. Aplicativos interoperáveis devem construir identificadores de acordo com esses valores.  
  
 Ao citar identificadores que contêm mais de uma parte, os aplicativos devem ter cuidado para fazer uma cotação de cada parte separadamente e não citar o caractere que separa os identificadores. Por exemplo, a instrução a seguir para selecionar todas as linhas e colunas de uma tabela Xbase aspas os nomes de catálogo (\XBASE\SALES\CORP) e tabela (Parts. dbf), mas não o separador de catálogo (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 A instrução a seguir para selecionar todas as linhas e colunas de uma tabela do Oracle marca os nomes catálogo (vendas), esquema (corporativo) e tabela (partes), mas não os separadores de catálogo (@) ou esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obter informações sobre como delimitar identificadores, consulte a próxima seção, [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).
