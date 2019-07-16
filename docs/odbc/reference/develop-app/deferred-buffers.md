---
title: Adiado Buffers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f7c90dacc375877b4e449b8d59533ce75ff8a4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076832"
---
# <a name="deferred-buffers"></a>Buffers adiados
Um *buffer adiada* é aquele cujo valor é usado em algum momento *depois* for especificado em uma chamada de função. Por exemplo, **SQLBindParameter** é usado para associar, ou *associar,* um buffer de dados com um parâmetro em uma instrução SQL. O aplicativo especifica o número do parâmetro e passa o endereço, o comprimento de bytes e o tipo de buffer. O driver salva essas informações, mas não examina o conteúdo do buffer. Posteriormente, quando o aplicativo executa a instrução, o driver recupera as informações e usa-o para recuperar os dados de parâmetro e enviá-lo para a fonte de dados. Portanto, a entrada de dados no buffer é adiada. Como buffers adiados são especificados em uma função e usados em outro, ele é um erro de programação de aplicativo ao liberar um buffer adiado, enquanto o driver ainda espera que ele exista; Para obter mais informações, consulte [alocando e liberando Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), mais adiante nesta seção.  
  
 Buffers de entrada e saídas podem ser adiadas. A tabela a seguir resume os usos dos buffers adiados. Observe que os buffers adiados associados a colunas do conjunto de resultados são especificados com **SQLBindCol**, e buffers adiados associados aos parâmetros de instrução SQL são especificados usando **SQLBindParameter**.  
  
|Uso de buffer|type|Especificado com|Usado por|  
|----------------|----------|--------------------|-------------|  
|Enviando dados para parâmetros de entrada|Entrada adiada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Enviando dados para atualizar ou inserir uma linha em um resultado definido|Entrada adiada|**SQLBindCol**|**SQLSetPos**|  
|Retornando dados de saída e parâmetros de entrada/saída|Saída adiada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Retornando resultados conjunto de dados|Saída adiada|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
