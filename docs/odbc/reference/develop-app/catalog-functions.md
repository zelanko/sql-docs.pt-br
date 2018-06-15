---
title: Funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 582b6d0912263d2eba76a7e357787c7c75ba0a75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911151"
---
# <a name="catalog-functions"></a>Funções de catálogo
Todos os bancos de dados têm uma estrutura que descreve como os dados serão armazenados no banco de dados. Por exemplo, um banco de dados de pedidos de vendas simples pode ter a estrutura mostrada na ilustração a seguir, na qual as colunas de ID são usadas para vincular as tabelas.  
  
 ![Mostra a estrutura de um banco de dados simple](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Essa estrutura, juntamente com outras informações como privilégios, é armazenada em um conjunto de tabelas do sistema chamado de banco de dados *catálogo,* que também é conhecido como um *dicionário de dados*.  
  
 Um aplicativo pode detectar essa estrutura por meio de chamadas para o *funções de catálogo*. As funções de catálogo retornam informações em conjuntos de resultados e são normalmente implementados por meio de **selecione** instruções em relação as tabelas do catálogo. Por exemplo, um aplicativo pode solicitar um conjunto de resultados que contém informações sobre todas as tabelas no sistema ou todas as colunas de uma tabela específica.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funções de catálogo em ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
