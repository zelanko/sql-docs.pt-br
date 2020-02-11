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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901274"
---
# <a name="executing-catalog-functions"></a>Executar funções de catálogo
Como uma função de catálogo cria um conjunto de resultados, é equivalente a executar qualquer instrução SQL que gere o conjunto de resultados. Na verdade, as funções de catálogo são geralmente implementadas executando instruções SQL predefinidas ou chamando procedimentos predefinidos que são fornecidos com o driver ou DBMS. Quase tudo que se aplica a instruções SQL que criam conjuntos de resultados também se aplica às funções de catálogo. Por exemplo, o atributo de instrução SQL_ATTR_MAX_ROWS limita o número de linhas retornadas pela função de catálogo, assim como limita o número de linhas retornadas por uma instrução **Select** .  
  
 Para executar uma função de catálogo, um aplicativo apenas chama a função.  
  
 Para obter mais informações sobre as funções de catálogo, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).
