---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: rothja
ms.author: jroth
ms.openlocfilehash: e5d44756131b6133baec69e34da11055a965e2da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022725"
---
# <a name="sqlendtran"></a>SQLEndTran
  Por padrão, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fecha o cursor associado de uma instrução quando **SQLEndTran** confirma ou reverte uma operação. Os cursores de servidor são fechados, a menos que eles sejam estáticos. Quando **SQLEndTran** confirma ou reverte uma operação, o comportamento do cursor associado da instrução é determinado pelo valor do atributo SQL_COPT_SS_PRESERVE_CURSORS da conexão ODBC específica do driver, definido por [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de implementação da API ODBC](odbc-api-implementation-details.md)   
 [Função SQLEndTran](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
