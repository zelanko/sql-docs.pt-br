---
title: Demonstrações geradoras de resultados e sem resultados | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300086"
---
# <a name="result-generating-and-result-free-statements"></a>Instruções de geração de resultado e sem resultados
As instruções SQL podem ser vagamente divididas nas cinco categorias a seguir:  
  
-   **Demonstrações geradoras de conjuntode resultados** Estas são instruções SQL que geram um conjunto de resultados. Por exemplo, uma declaração **SELECT.**  
  
-   **Demonstrações geradoras de contagem de linhas** Estas são instruções SQL que geram uma contagem de linhas afetadas. Por exemplo, uma **declaração UPDATE** ou **DELETE.**  
  
-   **Instruções de Linguagem de Definição de Dados (DDL)** Estas são instruções SQL que modificam a estrutura do banco de dados. Por exemplo, **CRIAR TABELA** ou **ÍNDICE DE QUEDA**.  
  
-   **Declarações que mudam o contexto** Estas são declarações SQL que mudam o contexto de um banco de dados. Por exemplo, as instruções **USE** e **SET** no SQL Server.  
  
-   **Declarações Administrativas** Estas são declarações SQL usadas para fins administrativos em um banco de dados. Por exemplo, **GRANT** e **REVOKE**.  
  
 As declarações sql nas duas primeiras categorias são coletivamente conhecidas como *declarações geradoras de resultados*. As declarações sql nas três últimas categorias são coletivamente conhecidas como *declarações livres de resultados*. A ODBC define a semântica dos lotes que incluem apenas declarações geradoras de resultados. Essas semânticas variam amplamente e, portanto, são específicas da fonte de dados. Por exemplo, o driver SQL Server não suporta soltar um objeto e, em seguida, referir-se ou recriar o mesmo objeto no mesmo lote. Portanto, o termo *lote* usado neste manual refere-se apenas a lotes de demonstrações geradoras de resultados.
