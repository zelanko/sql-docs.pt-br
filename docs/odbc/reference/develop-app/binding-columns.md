---
title: Colunas de associação | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02368c6294ab3eae345c756692cde83a1bc6aed6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="binding-columns"></a>Colunas de associação
Dados buscados da fonte de dados são retornados para o aplicativo em variáveis que o aplicativo foi alocado para essa finalidade. Antes de fazer isso, o aplicativo deve associar, ou *associar*, definir essas variáveis para as colunas do resultado, conceitualmente, esse processo é a mesma associação de variáveis de aplicativo para parâmetros de instrução. Quando o aplicativo associa uma variável para um conjunto de resultados coluna, ele descreve essa variável, endereço, tipo de dados e assim por diante — para o driver. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para retornar o valor da coluna quando a linha é procurada.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
