---
title: Executar funções de catálogo | Microsoft Docs
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
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 854a7e7fe347bb02c59fe1608afd74bf87be6b7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executing-catalog-functions"></a>Executar funções de catálogo
Como uma função de catálogo cria um conjunto de resultados, é equivalente a executar qualquer instrução de SQL de geração de conjunto de resultados. Na verdade, funções de catálogo geralmente são implementadas pela execução de instruções SQL predefinidas ou chamar procedimentos predefinidos que são fornecidos com o driver ou DBMS. Quase tudo o que se aplica às instruções SQL que cria conjuntos de resultados também se aplica a funções de catálogo. Por exemplo, o atributo da instrução SQL_ATTR_MAX_ROWS limita o número de linhas retornado pela função de catálogo, exatamente como ele limita o número de linhas retornadas por uma **selecione** instrução.  
  
 Para executar uma função de catálogo, um aplicativo apenas chama a função.  
  
 Para obter mais informações sobre funções de catálogo, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
