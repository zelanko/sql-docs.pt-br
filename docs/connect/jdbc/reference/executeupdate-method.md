---
title: Método executeUpdate () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eae73888b97b8511a23ba3387e2674bff40643c2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954583"
---
# <a name="executeupdate-method-"></a>Método executeUpdate ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL no objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que deve ser uma instrução SQL INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução DDL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número de linhas afetadas ou 0 se uma instrução DDL estiver sendo usada.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeUpdate é especificado pelo método executeUpdate na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método executeUpdate &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
