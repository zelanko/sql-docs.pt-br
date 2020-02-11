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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7cd157edd6111dec29ae238a1c383879e66ac0b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067428"
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
