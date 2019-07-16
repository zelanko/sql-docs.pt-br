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
ms.openlocfilehash: 55b2ff4d428f02b59883b675fde95531366f0b4d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020605"
---
# <a name="result-generating-and-result-free-statements"></a>Instruções de geração de resultado e sem resultados
Instruções SQL podem ser livremente divididas nas seguintes cinco categorias:  
  
-   **Resultar de geração de conjunto de instruções** essas são instruções SQL que geram um conjunto de resultados. Por exemplo, uma **selecionar** instrução.  
  
-   **Instruções de geração de contagem de linhas** essas são instruções SQL que geram uma contagem de linhas afetadas. Por exemplo, um **atualização** ou **excluir** instrução.  
  
-   **Data Definition Language (DDL) instruções** essas são instruções SQL que modificam a estrutura do banco de dados. Por exemplo, **CREATE TABLE** ou **DROP INDEX**.  
  
-   **Alterando o contexto de instruções** essas são instruções SQL que alterar o contexto de um banco de dados. Por exemplo, o **uso** e **definir** instruções no SQL Server.  
  
-   **Instruções administrativas** essas são instruções SQL usadas para fins administrativos em um banco de dados. Por exemplo, **GRANT** e **REVOGAR**.  
  
 Instruções SQL em que as duas primeiras categorias são coletivamente conhecidas como *instruções de geração de resultado*. Instruções SQL em três categorias de segundo são coletivamente conhecidas como *livres de resultado instruções*. ODBC define a semântica de lotes que incluem as instruções de apenas gerar resultados. Essa semântica variar muito e, portanto, específico de fonte de dados. Por exemplo, o driver do SQL Server não oferece suporte a descartar um objeto e, em seguida, referindo-se a ou recriando o mesmo objeto no mesmo lote. Portanto, o termo *lote* como usado deste manual refere-se somente a lotes de geração de resultado de instruções.
