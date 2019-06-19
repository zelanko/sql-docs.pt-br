---
title: Cursores estáticos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ddd2b4d998ab2718757db4dd58de6aea8bee05e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62799015"
---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Um cursor estático é um no qual o conjunto de resultados é exibido como estático. Ele geralmente não detectar alterações que foram feitas para a associação, pedido ou valores do conjunto de resultados depois que o cursor é aberto. Por exemplo, suponha que um cursor estático busca uma linha e o outro aplicativo, em seguida, atualiza a linha. Se o cursor estático refetches a linha, os que ele vê os valores são inalterados, apesar das alterações feitas por outro aplicativo.  
  
 Cursores estáticos podem detectar suas próprias atualizações, exclusões e inserções, embora eles não são necessários para fazer isso. Se um cursor estático particular detecta essas alterações é relatada com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**. Cursores estáticos detectam nunca outras atualizações, exclusões e inserções.  
  
 A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas atualizadas, excluídas ou inseridas pelo cursor, supondo que o cursor pode detectar essas alterações.  
  
 Cursores estáticos normalmente são implementados, bloqueando as linhas no conjunto de resultados ou fazendo uma cópia ou de instantâneo, do resultado definidos. Embora o bloqueio de linhas é relativamente fácil de fazer, ele tem a desvantagem de reduzir significativamente a simultaneidade. Fazer uma cópia permite maior simultaneidade e permite que o cursor para manter o controle de suas próprias atualizações, exclusões e insere modificando a cópia. No entanto, uma cópia é mais cara para fazer e podem divergir dos dados subjacentes, como esses dados são alterados por outras pessoas.
