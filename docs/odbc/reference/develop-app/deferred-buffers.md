---
description: Buffers adiados
title: Buffers adiados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 320271c39c735eafcfb1d59d26e7d0400eaa6e6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424698"
---
# <a name="deferred-buffers"></a>Buffers adiados
Um *buffer adiado* é aquele cujo valor é usado em algum momento *depois* de ser especificado em uma chamada de função. Por exemplo, **SQLBindParameter** é usado para *associar ou associar um buffer de dados* a um parâmetro em uma instrução SQL. O aplicativo especifica o número do parâmetro e passa o endereço, o comprimento do byte e o tipo do buffer. O driver salva essas informações, mas não examina o conteúdo do buffer. Posteriormente, quando o aplicativo executar a instrução, o driver recuperará as informações e as usará para recuperar os dados do parâmetro e enviá-los para a fonte de dados. Portanto, a entrada de dados no buffer é adiada. Como os buffers adiados são especificados em uma função e usados em outro, é um erro de programação de aplicativo liberar um buffer adiado enquanto o driver ainda espera que ele exista; para obter mais informações, consulte [alocando e liberando buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), mais adiante nesta seção.  
  
 Os buffers de entrada e de saída podem ser adiados. A tabela a seguir resume os usos de buffers adiados. Observe que os buffers adiados associados às colunas do conjunto de resultados são especificados com **SQLBindCol**, e os buffers adiados associados aos parâmetros da instrução SQL são especificados com **SQLBindParameter**.  
  
|Uso do buffer|Type|Especificado com|Usado por|  
|----------------|----------|--------------------|-------------|  
|Enviando dados para parâmetros de entrada|Entrada adiada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Enviando dados para atualizar ou inserir uma linha em um conjunto de resultados|Entrada adiada|**SQLBindCol**|**SQLSetPos**|  
|Retornando dados para saída e parâmetros de entrada/saída|Saída adiada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Retornando dados do conjunto de resultados|Saída adiada|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
