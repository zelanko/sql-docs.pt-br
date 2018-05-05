---
title: Método (SQLServerResultSet) Finalize | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: 7cbbef1a1a3ee4d45d089ba13aec873153b1a141
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
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
  
  
