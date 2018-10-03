---
title: Método Finalize (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e1b8a5435d6923015c2d3c29eef5031f3d5b2f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622784"
---
# <a name="finalize-method-sqlserverresultset"></a>Método finalize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fecha explicitamente o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Remarks  
 Fecha o conjunto de resultados se o aplicativo não o fizer. Esse método existe apenas para conformidade com a especificação JDBC. Como a JVM (Máquina Virtual Java) não garante quando um finalizador terá uma chance de ser executado, os aplicativos que esquecem de fechar explicitamente seus respectivos conjuntos de resultados ainda podem usar o deadlock em outra instrução que esteja usando a mesma conexão e seja bloqueada em um recurso de servidor comum, como bloqueios de linha.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
