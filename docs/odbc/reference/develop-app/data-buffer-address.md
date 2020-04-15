---
title: Endereço de buffer de dados | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305267"
---
# <a name="data-buffer-address"></a>Endereço do buffer de dados
O aplicativo passa o endereço do buffer de dados para o driver em um argumento, muitas vezes chamado *ValuePtr* ou um nome semelhante. Por exemplo, na seguinte chamada para **SQLBindCol,** o aplicativo especifica o endereço da variável *Data:*  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Como mencionado na [seção Alocando e Liberando Buffers,](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) o endereço de um buffer diferido deve permanecer válido até que o buffer seja desvinculado.  
  
 A menos que seja especificamente proibido, o endereço de um buffer de dados pode ser um ponteiro nulo. Para buffers usados para enviar dados ao driver, isso faz com que o motorista ignore as informações normalmente contidas no buffer. Para buffers usados para recuperar dados do driver, isso faz com que o motorista não devolva um valor. Em ambos os casos, o driver ignora o argumento de comprimento do buffer de dados correspondente.
