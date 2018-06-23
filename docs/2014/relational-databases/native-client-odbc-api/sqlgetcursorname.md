---
title: SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6262c913a0b7f3060b0c48f9061cab90345f99ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008644"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
  Se o aplicativo não especificar um nome de cursor, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client irá gerar um nome durante a criação do cursor. O aplicativo pode usar **SQLGetCursorName** para recuperar o nome de cursor definido pelo driver para as instruções UPDATE e DELETE posicionadas. O aplicativo não precisa chamar **SQLSetCursorName** para aproveitar as instruções de manipulação de dados posicionadas.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLGetCursorName](http://go.microsoft.com/fwlink/?LinkId=59349)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  