---
title: "Método setFetchDirection (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dd6ab9a94acf883ed27cdd79fee886b6c54ca596
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setfetchdirection-method-sqlserverresultset"></a>Método setFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornece uma dica sobre a direção na qual as linhas na [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto será processado.  
  
> [!NOTE]  
>  Esse método não é suportado atualmente pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se você usar este método, o driver JDBC se lembrará da configuração, mas atualmente ele não age em função dela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *direção*  
  
 Um **int** que indica a direção de busca sugerida. Pode ser um dos seguintes valores:  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setFetchDirection é especificado pelo método setFetchDirection na interface Java.SQL. resultset.  
  
 O valor inicial deste método é determinado pelo [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que produziu o objeto SQLServerResultSet. A direção de busca pode ser alterada a qualquer momento.  
  
> [!NOTE]  
>  Usar este método quando o tipo de cursor é somente encaminhamento não tem nenhum efeito.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
