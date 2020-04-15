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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6469a5394e232ab9d9135fbbbd56ba7b791ccbcb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305717"
---
# <a name="executing-catalog-functions"></a>Executar funções de catálogo
Como uma função de catálogo cria um conjunto de resultados, ela é equivalente à execução de qualquer demonstração SQL de geração de resultados. Na verdade, as funções de catálogo são frequentemente implementadas executando declarações SQL predefinidas ou chamando procedimentos predefinidos que são enviados com o driver ou DBMS. Quase tudo o que se aplica às instruções SQL que criam conjuntos de resultados também se aplica às funções de catálogo. Por exemplo, o atributo de declaração SQL_ATTR_MAX_ROWS limita o número de linhas retornadas pela função catálogo, assim como limita o número de linhas retornadas por uma declaração **SELECT.**  
  
 Para executar uma função de catálogo, um aplicativo apenas chama a função.  
  
 Para obter mais informações sobre funções de catálogo, consulte [Funções do Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
