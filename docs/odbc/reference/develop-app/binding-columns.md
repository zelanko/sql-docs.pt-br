---
title: Vinculando colunas | Microsoft Docs
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
ms.openlocfilehash: a634a553672b83931091056dd489f7559c4269b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106211"
---
# <a name="binding-columns"></a>Colunas de associação
Os dados buscados da fonte de dados são retornados para o aplicativo em variáveis que o aplicativo alocou para essa finalidade. Antes que isso possa ser feito, o aplicativo deve *associar ou associar*essas variáveis às colunas do conjunto de resultados; Conceitualmente, esse processo é o mesmo que associar variáveis de aplicativo a parâmetros de instrução. Quando o aplicativo associa uma variável a uma coluna de conjunto de resultados, ele descreve o endereço variável, o tipo de dados e assim por diante – para o driver. O driver armazena essas informações na estrutura que ela mantém para essa instrução e usa as informações para retornar o valor da coluna quando a linha é buscada.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Associar colunas de conjunto de resultados](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Usar SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
