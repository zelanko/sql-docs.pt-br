---
title: Método rowDeleted (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37221f0f9c7cf87576f0014b855ed28740e4818e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975707"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>Método rowDeleted (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se uma linha foi excluída.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se uma linha tiver sido excluída e as exclusões forem detectadas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método de exclusão é especificado pelo método de exclusão na interface java. Sql. ResultSet.  
  
 Uma linha excluída pode deixar um buraco visível em um conjunto de resultados. Esse método pode ser usado para detectar buracos em um conjunto de resultados. O valor retornado dependerá da capacidade do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de detectar exclusões.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detecta linhas excluídas de todos os tipos de cursores atualizáveis, embora a detecção seja transitória para cursores dinâmicos e de avanço.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
