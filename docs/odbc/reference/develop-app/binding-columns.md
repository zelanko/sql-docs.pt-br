---
title: Colunas de Vinculação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fca4cfb1455c91ca57f7b1769266e2040d6a3511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301817"
---
# <a name="binding-columns"></a>Colunas de associação
Os dados obtidos na fonte de dados são devolvidos ao aplicativo em variáveis que o aplicativo alocou para este fim. Antes que isso possa ser feito, o aplicativo deve associar, ou *vincular,* essas variáveis às colunas do conjunto de resultados; conceitualmente, esse processo é o mesmo que variáveis de aplicação vinculantes aos parâmetros de declaração. Quando o aplicativo vincula uma variável a uma coluna de conjunto de resultados, ele descreve essa variável - endereço, tipo de dados e assim por diante - ao driver. O motorista armazena essas informações na estrutura que mantém para essa declaração e usa as informações para devolver o valor da coluna quando a linha é buscada.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Associar colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usar SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
