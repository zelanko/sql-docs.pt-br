---
title: Método (SQLServerResultSet) rowDeleted | Microsoft Docs
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
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49dc624ba683d41f527780c69204aadd9b2a51b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted método (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se uma linha foi excluída.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se uma linha foi excluída e as exclusões forem detectadas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método rowDeleted é especificado pelo método rowDeleted na interface Java.SQL. resultset.  
  
 Uma linha excluída pode deixar um buraco visível em um conjunto de resultados. Esse método pode ser usado para detectar buracos em um conjunto de resultados. O valor retornado depende se isso [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto pode detectar exclusões.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] detecta linhas excluídas para todos os tipos de cursores atualizáveis, embora a detecção seja transitória para cursores dinâmicos e de avanço.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
