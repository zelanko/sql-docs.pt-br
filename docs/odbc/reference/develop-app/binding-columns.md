---
title: "Colunas de associação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5903070b8918baa9734e5d188d90861322b57986
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="binding-columns"></a>Colunas de associação
Dados buscados da fonte de dados são retornados para o aplicativo em variáveis que o aplicativo foi alocado para essa finalidade. Antes de fazer isso, o aplicativo deve associar, ou *associar*, definir essas variáveis para as colunas do resultado, conceitualmente, esse processo é a mesma associação de variáveis de aplicativo para parâmetros de instrução. Quando o aplicativo associa uma variável para um conjunto de resultados coluna, ele descreve essa variável, endereço, tipo de dados e assim por diante — para o driver. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para retornar o valor da coluna quando a linha é procurada.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)

