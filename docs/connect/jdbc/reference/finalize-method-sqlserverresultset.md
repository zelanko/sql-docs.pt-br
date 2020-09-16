---
description: Método finalize (SQLServerResultSet)
title: Método finalize (SQLServerResultSet) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6f232e7755dd975edaa7b255e5ffe6dd9f85091
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437588"
---
# <a name="finalize-method-sqlserverresultset"></a>Método finalize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fecha explicitamente o objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Comentários  
 Fecha o conjunto de resultados se o aplicativo não o fizer. Esse método existe apenas para conformidade com a especificação JDBC. Como a JVM (Máquina Virtual Java) não garante quando um finalizador terá uma chance de ser executado, os aplicativos que esquecem de fechar explicitamente seus respectivos conjuntos de resultados ainda podem usar o deadlock em outra instrução que esteja usando a mesma conexão e seja bloqueada em um recurso de servidor comum, como bloqueios de linha.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
