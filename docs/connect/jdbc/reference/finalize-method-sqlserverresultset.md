---
title: Método (SQLServerResultSet) Finalize | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56c7131bfc0b5f1bb293b7a697f090495f0938f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="finalize-method-sqlserverresultset"></a>finalizar o método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fecha explicitamente isso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Remarks  
 Fecha o conjunto de resultados se o aplicativo não o fizer. Esse método existe apenas para conformidade com a especificação JDBC. Como a JVM (Máquina Virtual Java) não garante quando um finalizador terá uma chance de ser executado, os aplicativos que esquecem de fechar explicitamente seus respectivos conjuntos de resultados ainda podem usar o deadlock em outra instrução que esteja usando a mesma conexão e seja bloqueada em um recurso de servidor comum, como bloqueios de linha.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
