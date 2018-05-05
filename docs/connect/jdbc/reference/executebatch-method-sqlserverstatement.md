---
title: Método (SQLServerStatement) executeBatch | Microsoft Docs
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
- SQLServerStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb034f63-2532-4da8-a1b0-bc125734585a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb25a65508e2249a71e67e4db3f3e762476f33df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executebatch-method-sqlserverstatement"></a>executeBatch método (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Envia um lote de comandos ao banco de dados a ser executado. Se todos os comandos forem executados com êxito, uma matriz de contagens de atualização será retornada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Uma matriz de **int**que contém a atualização de conta.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Remarks  
 Esse método executeBatch é especificado pelo método executeBatch na interface Java.SQL. Statement.  
  
 Depois de enviar comandos ao banco de dados, esse método limpa qualquer comando no lote.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
