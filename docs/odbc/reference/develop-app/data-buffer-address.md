---
title: Endereço do buffer de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578e4e37a78818cb640d9f32e2480cec5951df63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305267"
---
# <a name="data-buffer-address"></a>Endereço do buffer de dados
O aplicativo passa o endereço do buffer de dados para o driver em um argumento, geralmente chamado de *ValuePtr* ou um nome semelhante. Por exemplo, na chamada a seguir para **SQLBindCol**, o aplicativo especifica o endereço da variável *Date* :  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Conforme mencionado na seção [alocando e liberando buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) , o endereço de um buffer adiado deve permanecer válido até que o buffer seja desassociado.  
  
 A menos que seja especificamente proibido, o endereço de um buffer de dados pode ser um ponteiro nulo. Para buffers usados para enviar dados ao driver, isso faz com que o driver ignore as informações normalmente contidas no buffer. Para buffers usados para recuperar dados do driver, isso faz com que o driver não retorne um valor. Em ambos os casos, o driver ignora o argumento de comprimento do buffer de dados correspondente.
