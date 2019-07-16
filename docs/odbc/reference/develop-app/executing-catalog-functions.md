---
title: Executando funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab6eba9c4a3df3e16e35d8a93dc95209a093fb80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901274"
---
# <a name="executing-catalog-functions"></a>Executar funções de catálogo
Como uma função de catálogo cria um conjunto de resultados, é equivalente a executar qualquer instrução de SQL de geração de conjunto de resultados. Na verdade, funções de catálogo geralmente são implementadas por execução de instruções de SQL predefinidas ou chamar procedimentos predefinidos que são fornecidos com o driver ou DBMS. Quase tudo o que se aplica a instruções SQL que cria conjuntos de resultados também se aplica a funções de catálogo. Por exemplo, o atributo da instrução SQL_ATTR_MAX_ROWS limita o número de linhas retornadas pela função de catálogo, exatamente como ele limita o número de linhas retornadas por uma **selecionar** instrução.  
  
 Para executar uma função de catálogo, um aplicativo simplesmente chama a função.  
  
 Para obter mais informações sobre funções de catálogo, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
