---
description: Executar funções de catálogo
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
ms.openlocfilehash: 19baae1518078c44b8e170fb623eab0087bac12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482909"
---
# <a name="executing-catalog-functions"></a>Executar funções de catálogo
Como uma função de catálogo cria um conjunto de resultados, é equivalente a executar qualquer instrução SQL que gere o conjunto de resultados. Na verdade, as funções de catálogo são geralmente implementadas executando instruções SQL predefinidas ou chamando procedimentos predefinidos que são fornecidos com o driver ou DBMS. Quase tudo que se aplica a instruções SQL que criam conjuntos de resultados também se aplica às funções de catálogo. Por exemplo, o atributo de instrução SQL_ATTR_MAX_ROWS limita o número de linhas retornadas pela função de catálogo, assim como limita o número de linhas retornadas por uma instrução **Select** .  
  
 Para executar uma função de catálogo, um aplicativo apenas chama a função.  
  
 Para obter mais informações sobre as funções de catálogo, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).
