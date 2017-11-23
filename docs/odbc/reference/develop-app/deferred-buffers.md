---
title: Adiado Buffers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3af1222c7404a5b05246026edbbc37149780de8c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="deferred-buffers"></a>Buffers adiadas
Um *buffer adiada* é uma cujo valor é usado em algum momento *depois* for especificado em uma chamada de função. Por exemplo, **SQLBindParameter** é usada para associar, ou *associar,* um buffer de dados com um parâmetro em uma instrução SQL. O aplicativo especifica o número do parâmetro e passa o endereço, o comprimento em bytes e o tipo de buffer. O driver salva essas informações, mas não examina o conteúdo do buffer. Posteriormente, quando o aplicativo executa a instrução, o driver recupera as informações e o utiliza para recuperar os dados de parâmetro e enviá-lo à fonte de dados. Portanto, a entrada de dados no buffer é adiada. Como buffers adiadas são especificados em uma função e usados em outra, é um erro de programação de aplicativo para liberar um buffer adiado, enquanto o driver ainda espera existe; Para obter mais informações, consulte [Allocating e liberar Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), mais adiante nesta seção.  
  
 Buffers de entrada e saídas podem ser adiadas. A tabela a seguir resume os usos dos buffers adiadas. Observe que adiada buffers associados a colunas do conjunto de resultados são especificadas com **SQLBindCol**, e adiadas buffers associados aos parâmetros de instrução SQL são especificados com **SQLBindParameter**.  
  
|Uso de buffer|Tipo|Especificado com|Usado por|  
|----------------|----------|--------------------|-------------|  
|Enviando dados para parâmetros de entrada|Entrada adiada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Enviar dados para atualizar ou inserir uma linha em um resultado definido|Entrada adiada|**SQLBindCol**|**SQLSetPos**|  
|Retornando dados de saída e parâmetros de entrada/saída|Saída adiada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Retornar resultados conjunto de dados|Saída adiada|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
