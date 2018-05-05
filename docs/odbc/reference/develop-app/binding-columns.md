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
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c19d922cfce67c50e8dfbfcfe7d2fb1729250199
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-columns"></a>Colunas de associação
Dados buscados da fonte de dados são retornados para o aplicativo em variáveis que o aplicativo foi alocado para essa finalidade. Antes de fazer isso, o aplicativo deve associar, ou *associar*, definir essas variáveis para as colunas do resultado, conceitualmente, esse processo é a mesma associação de variáveis de aplicativo para parâmetros de instrução. Quando o aplicativo associa uma variável para um conjunto de resultados coluna, ele descreve essa variável, endereço, tipo de dados e assim por diante — para o driver. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para retornar o valor da coluna quando a linha é procurada.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
