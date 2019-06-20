---
title: Instruções de geração de resultado e sem | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f357576e9e7510ae581b41a50976a34981f35109
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861516"
---
# <a name="result-generating-and-result-free-statements"></a>Instruções de geração de resultado e sem resultados
Instruções SQL podem ser livremente divididas nas seguintes cinco categorias:  
  
-   **Resultar de geração de conjunto de instruções** essas são instruções SQL que geram um conjunto de resultados. Por exemplo, uma **selecionar** instrução.  
  
-   **Instruções de geração de contagem de linhas** essas são instruções SQL que geram uma contagem de linhas afetadas. Por exemplo, um **atualização** ou **excluir** instrução.  
  
-   **Data Definition Language (DDL) instruções** essas são instruções SQL que modificam a estrutura do banco de dados. Por exemplo, **CREATE TABLE** ou **DROP INDEX**.  
  
-   **Alterando o contexto de instruções** essas são instruções SQL que alterar o contexto de um banco de dados. Por exemplo, o **uso** e **definir** instruções no SQL Server.  
  
-   **Instruções administrativas** essas são instruções SQL usadas para fins administrativos em um banco de dados. Por exemplo, **GRANT** e **REVOGAR**.  
  
 Instruções SQL em que as duas primeiras categorias são coletivamente conhecidas como *instruções de geração de resultado*. Instruções SQL em três categorias de segundo são coletivamente conhecidas como *livres de resultado instruções*. ODBC define a semântica de lotes que incluem as instruções de apenas gerar resultados. Essa semântica variar muito e, portanto, específico de fonte de dados. Por exemplo, o driver do SQL Server não oferece suporte a descartar um objeto e, em seguida, referindo-se a ou recriando o mesmo objeto no mesmo lote. Portanto, o termo *lote* como usado deste manual refere-se somente a lotes de geração de resultado de instruções.
