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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282436"
---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Um cursor estático é aquele em que o conjunto de resultados parece estar estático. Ele não costuma detectar alterações que foram feitas na adesão, ordem ou valores do resultado definido após a abertura do cursor. Por exemplo, suponha que um cursor estático busque uma linha e outro aplicativo, em seguida, atualiza essa linha. Se o cursor estático rebusca a linha, os valores que ele vê são inalterados, apesar das alterações que foram feitas pela outra aplicação.  
  
 Os cursores estáticos podem detectar suas próprias atualizações, exclusões e inserções, embora não sejam obrigados a fazer isso. Se um cursor estático específico detecta essas alterações é relatado através da opção SQL_STATIC_SENSITIVITY no **SQLGetInfo**. Os cursores estáticos nunca detectam outras atualizações, exclusões e inserções.  
  
 A matriz de status da linha especificada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas atualizadas, excluídas ou inseridas pelo cursor, assumindo que o cursor possa detectar tais alterações.  
  
 Os cursores estáticos são normalmente implementados bloqueando as linhas no conjunto de resultados ou fazendo uma cópia, ou instantâneo, do conjunto de resultados. Embora as linhas de bloqueio sejam relativamente fáceis de fazer, ela tem a desvantagem de reduzir significativamente a concorrência. Fazer uma cópia permite uma maior concorrência e permite que o cursor acompanhe suas próprias atualizações, exclusões e inserções modificando a cópia. No entanto, uma cópia é mais cara de fazer e pode divergir dos dados subjacentes à medida que esses dados são alterados por outros.
