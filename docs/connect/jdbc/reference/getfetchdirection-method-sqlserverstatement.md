---
title: Método getFetchDirection (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 402aa6188af49690582c34e9883218cccf8e03a2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768889"
---
# <a name="getfetchdirection-method-sqlserverstatement"></a>Método getFetchDirection (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a direção para efetuar fetch em linhas de tabelas de banco de dados que é o padrão para conjuntos de resultados que são gerados deste objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
> [!NOTE]  
>  No momento, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não implementa esse método. Portanto, ele sempre retornará FETCH_UNKNOWN.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica a direção de fetch que é especificada pelo método [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md).  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getFetchDirection é especificado pelo método getFetchDirection na interface Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
