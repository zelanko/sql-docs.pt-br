---
title: "Cursores estáticos ODBC | Microsoft Docs"
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
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aaddef08bfea9e1a1820727743e5212557d823d4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Um cursor estático é um no qual o conjunto de resultados parece ser estático. Ele geralmente não detectar alterações que foram feitas para a associação, ordem ou valores do conjunto de resultados depois que o cursor é aberto. Por exemplo, suponha que um cursor estático busca uma linha e outro aplicativo, em seguida, atualiza a linha. Se o cursor estático refetches a linha, os valores que ele vê são inalterados, apesar das alterações feitas por outro aplicativo.  
  
 Cursores estáticos podem detectar suas próprias atualizações, exclusões e inserções, embora eles não são necessários para fazer isso. Se um cursor estático específico detecta essas alterações é relatado com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**. Cursores estáticos nunca detectam outros atualiza, exclui e insere.  
  
 A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas atualizadas, excluídas ou inseridas pelo cursor, supondo que o cursor pode detectar essas alterações.  
  
 Cursores estáticos são normalmente implementados por meio do bloqueio de linhas no conjunto de resultados ou fazendo uma cópia ou de instantâneo, do resultado definidos. Embora o bloqueio de linhas é relativamente fácil de fazer, ele tem a desvantagem de reduzir significativamente a simultaneidade. Fazer uma cópia permite maior simultaneidade e permite que o cursor controlar suas próprias atualizações, exclusões e insere modificando a cópia. No entanto, uma cópia é mais cara para fazer e pode divergem dos dados subjacentes que esses dados são alterados por outras pessoas.

