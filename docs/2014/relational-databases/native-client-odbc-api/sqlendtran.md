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
manager: craigg
ms.openlocfilehash: ec3c40d7821c86f3f5c5a7eb0d63ab48904513e2
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706270"
---
# <a name="sqlendtran"></a>SQLEndTran
  Por padrão, o driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fecha o cursor associado de uma instrução quando **SQLEndTran** confirma ou reverte uma operação. Os cursores de servidor são fechados, a menos que eles sejam estáticos. Quando **SQLEndTran** confirma ou reverte uma operação, o comportamento do cursor associado da instrução é determinado pelo valor do atributo SQL_COPT_SS_PRESERVE_CURSORS da conexão ODBC específica do driver, definido por [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de implementação da API ODBC](odbc-api-implementation-details.md)   
 [Função SQLEndTran](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
