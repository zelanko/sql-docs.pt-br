---
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ba100363f3570364d9a114e8406d2b0b4c8f21f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411755"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  No modo de confirmação manual, chamar **SQLFreeHandle** em um identificador de instrução com uma transação aberta causará uma reversão das alterações pendentes do banco de dados. Chamar **SQLFreeHandle** em um identificador de instrução sempre fechará quaisquer cursores abertos e descartará resultados pendentes, liberando todos os recursos associados ao identificador de instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLFreeHandle](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
