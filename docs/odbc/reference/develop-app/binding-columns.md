---
title: Colunas de associação | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 035e525116622a3c55e50547958b86fc2ee9bdb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678344"
---
# <a name="binding-columns"></a>Colunas de associação
Os dados buscados da fonte de dados são retornados para o aplicativo em variáveis que o aplicativo alocado para essa finalidade. Antes de fazer isso, o aplicativo deve associar, ou *associar*, defina essas variáveis para as colunas de resultado; conceitualmente, esse processo é o mesmo que associando variáveis de aplicativo para parâmetros de instrução. Quando o aplicativo associa uma variável para um conjunto de resultados coluna, ele descreve essa variável, endereço, tipo de dados e assim por diante — para o driver. O driver armazena essas informações na estrutura, ele mantém para essa instrução e usa as informações para retornar o valor da coluna quando a linha é buscada.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Associando colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
