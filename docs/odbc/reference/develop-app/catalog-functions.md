---
title: Funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9f6b9990799027270c913cb332ce5a0ffc71171
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions"></a>Funções de catálogo
Todos os bancos de dados têm uma estrutura que descreve como os dados serão armazenados no banco de dados. Por exemplo, um banco de dados de pedidos de vendas simples pode ter a estrutura mostrada na ilustração a seguir, na qual as colunas de ID são usadas para vincular as tabelas.  
  
 ![Mostra a estrutura de um banco de dados simple](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Essa estrutura, juntamente com outras informações como privilégios, é armazenada em um conjunto de tabelas do sistema chamado de banco de dados *catálogo,* que também é conhecido como um *dicionário de dados*.  
  
 Um aplicativo pode detectar essa estrutura por meio de chamadas para o *funções de catálogo*. As funções de catálogo retornam informações em conjuntos de resultados e são normalmente implementados por meio de **selecione** instruções em relação as tabelas do catálogo. Por exemplo, um aplicativo pode solicitar um conjunto de resultados que contém informações sobre todas as tabelas no sistema ou todas as colunas de uma tabela específica.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funções de catálogo em ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
