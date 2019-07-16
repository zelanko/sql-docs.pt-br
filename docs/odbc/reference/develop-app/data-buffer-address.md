---
title: Endereço do Buffer de dados | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067428"
---
# <a name="data-buffer-address"></a>Endereço do buffer de dados
O aplicativo passa o endereço do buffer de dados para o driver em um argumento, geralmente denominado *ValuePtr* ou um nome semelhante. Por exemplo, na seguinte chamada para **SQLBindCol**, o aplicativo especifica o endereço do *data* variável:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Conforme mencionado na [alocando e liberando Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) seção, o endereço de um buffer adiado deve permanecer válido até que o buffer não está associado.  
  
 A menos que especificamente é proibido, o endereço de um buffer de dados pode ser um ponteiro nulo. Para buffers usados para enviar dados para o driver, isso faz com que o driver ignorar as informações normalmente contidas no buffer. Para os buffers usados para recuperar dados do driver, isso faz com que o driver não retornar um valor. Em ambos os casos, o driver ignorará o argumento de comprimento de buffer de dados correspondente.
