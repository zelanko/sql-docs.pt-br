---
title: Funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 268d5f00d787cef8dfdcb29bd9e091f81a5ed2c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125573"
---
# <a name="catalog-functions"></a>Funções de catálogo
Todos os bancos de dados têm uma estrutura que descreve como os dados serão armazenados no banco de dados. Por exemplo, um banco de dados do pedido de vendas simples pode ter a estrutura mostrada na ilustração a seguir, na qual as colunas do ID são usadas para vincular as tabelas.  
  
 ![Mostra a estrutura de um banco de dados simple](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Essa estrutura, juntamente com outras informações como privilégios, é armazenada em um conjunto de tabelas do sistema chamado de banco de dados *catálogo,* que é também conhecido como um *dicionário de dados*.  
  
 Um aplicativo pode descobrir essa estrutura por meio de chamadas para o *funções de catálogo*. As funções de catálogo retornam informações de conjuntos de resultados e são normalmente implementados por meio **selecionar** instruções nas tabelas no catálogo. Por exemplo, um aplicativo pode solicitar um conjunto de resultados que contém informações sobre todas as tabelas no sistema ou todas as colunas de uma tabela específica.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Funções de catálogo em ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
