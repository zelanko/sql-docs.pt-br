---
title: Instruções de geração de resultados e de resultado livre | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc94aabd7982fba5879519573980db03b1857ef6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300086"
---
# <a name="result-generating-and-result-free-statements"></a>Instruções de geração de resultado e sem resultados
As instruções SQL podem ser divididas livremente nas cinco categorias a seguir:  
  
-   **Instruções de geração de conjunto de resultados** Essas são instruções SQL que geram um conjunto de resultados. Por exemplo, uma instrução **Select** .  
  
-   **Contagem de linhas – gerando instruções** Essas são instruções SQL que geram uma contagem de linhas afetadas. Por exemplo, uma instrução **Update** ou **delete** .  
  
-   **Instruções DDL (linguagem de definição de dados)** Essas são instruções SQL que modificam a estrutura do banco de dados. Por exemplo, **CREATE TABLE** ou **drop index**.  
  
-   **Instruções de alteração de contexto** Essas são instruções SQL que alteram o contexto de um banco de dados. Por exemplo, as instruções **use** e **set** em SQL Server.  
  
-   **Instruções administrativas** Essas são instruções SQL usadas para fins administrativos em um banco de dados. Por exemplo, **Grant** e **REVOKE**.  
  
 As instruções SQL nas duas primeiras categorias são coletivamente conhecidas como *instruções de geração de resultados*. As instruções SQL nas últimas três categorias são coletivamente conhecidas como *instruções livres de resultado*. O ODBC define a semântica de lotes que incluem apenas instruções de geração de resultados. Essas semânticas variam muito e, portanto, são específicas da fonte de dados. Por exemplo, o driver SQL Server não oferece suporte a descartar um objeto e, em seguida, referir ou recriar o mesmo objeto no mesmo lote. Portanto, o termo *lote* como usado neste manual refere-se apenas a lotes de instruções que geram resultados.
