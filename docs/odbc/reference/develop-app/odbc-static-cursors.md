---
description: Cursores estáticos ODBC
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
ms.openlocfilehash: 9689badd39e21f82c268be904b29ffb1fa90a8ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429158"
---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Um cursor estático é aquele em que o conjunto de resultados parece ser estático. Geralmente, ele não detecta alterações que foram feitas na associação, na ordem ou nos valores do conjunto de resultados depois que o cursor é aberto. Por exemplo, suponha que um cursor estático busque uma linha e outro aplicativo, em seguida, atualize essa linha. Se o cursor estático rebuscar a linha, os valores que ela vê serão inalterados, apesar das alterações feitas pelo outro aplicativo.  
  
 Cursores estáticos podem detectar suas próprias atualizações, exclusões e inserções, embora não sejam obrigadas a fazer isso. Se um cursor estático específico detectar essas alterações é relatado por meio da opção SQL_STATIC_SENSITIVITY em **SQLGetInfo**. Cursores estáticos nunca detectam outras atualizações, exclusões e inserções.  
  
 A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas atualizadas, excluídas ou inseridas pelo cursor, supondo que o cursor possa detectar essas alterações.  
  
 Cursores estáticos são normalmente implementados bloqueando as linhas no conjunto de resultados ou fazendo uma cópia, ou instantâneo, do conjunto de resultados. Embora as linhas de bloqueio sejam relativamente fáceis de fazer, ela tem a desvantagem de reduzir significativamente a simultaneidade. Fazer uma cópia permite uma simultaneidade maior e permite que o cursor Mantenha o controle de suas próprias atualizações, exclusões e inserções modificando a cópia. No entanto, uma cópia é mais cara para fazer e pode divergir dos dados subjacentes, pois esses dados são alterados por outras pessoas.
