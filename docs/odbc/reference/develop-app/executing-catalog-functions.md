---
title: "Executar funções de catálogo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ffd7e2a1141f1ad474a899d00a9880849c9aef0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="executing-catalog-functions"></a>Executar funções de catálogo
Como uma função de catálogo cria um conjunto de resultados, é equivalente a executar qualquer instrução de SQL de geração de conjunto de resultados. Na verdade, funções de catálogo geralmente são implementadas pela execução de instruções SQL predefinidas ou chamar procedimentos predefinidos que são fornecidos com o driver ou DBMS. Quase tudo o que se aplica às instruções SQL que cria conjuntos de resultados também se aplica a funções de catálogo. Por exemplo, o atributo da instrução SQL_ATTR_MAX_ROWS limita o número de linhas retornado pela função de catálogo, exatamente como ele limita o número de linhas retornadas por uma **selecione** instrução.  
  
 Para executar uma função de catálogo, um aplicativo apenas chama a função.  
  
 Para obter mais informações sobre funções de catálogo, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
