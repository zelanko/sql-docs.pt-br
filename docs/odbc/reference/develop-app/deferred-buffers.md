---
title: Buffers diferidos | Microsoft Docs
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
ms.openlocfilehash: f34c6d3d886a0a75c309dc4f5c71f5c7ba3df447
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305977"
---
# <a name="deferred-buffers"></a>Buffers adiados
Um *buffer diferido* é aquele cujo valor é usado em algum momento *depois* de especificado em uma chamada de função. Por exemplo, **SQLBindParameter** é usado para associar, ou *vincular,* um buffer de dados com um parâmetro em uma declaração SQL. O aplicativo especifica o número do parâmetro e passa o endereço, o comprimento do byte e o tipo do buffer. O driver salva essas informações, mas não examina o conteúdo do buffer. Mais tarde, quando o aplicativo executa a declaração, o motorista recupera as informações e as usa para recuperar os dados do parâmetro e enviá-los para a fonte de dados. Portanto, a entrada de dados no buffer é adiada. Como os buffers diferidos são especificados em uma função e usados em outra, é um erro de programação de aplicativo para liberar um buffer diferido enquanto o driver ainda espera que ele exista; para obter mais informações, consulte [Alocando e Liberando Buffers,](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)mais tarde nesta seção.  
  
 Tanto os buffers de entrada quanto de saída podem ser adiados. A tabela a seguir resume os usos de buffers diferidos. Observe que os buffers diferidos vinculados às colunas de conjunto de resultados são especificados com **SQLBindCol**e os buffers diferidos vinculados aos parâmetros de declaração SQL são especificados com **SQLBindParameter**.  
  
|Uso de buffer|Type|Especificado com|Usado por|  
|----------------|----------|--------------------|-------------|  
|Envio de dados para parâmetros de entrada|Entrada diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Enviar dados para atualizar ou inserir uma linha em um conjunto de resultados|Entrada diferida|**SQLBindCol**|**SQLSetPos**|  
|Retornar dados para parâmetros de saída e entrada/saída|Saída diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Devolução de dados do conjunto de resultados|Saída diferida|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
