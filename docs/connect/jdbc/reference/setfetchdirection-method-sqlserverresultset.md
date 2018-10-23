---
title: Método setFetchDirection (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e725eb2bf07c587d04cf660917b9d0b70bf5cff3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695814"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>Método setFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornece uma dica sobre a direção em que as linhas no objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) serão processadas.  
  
> [!NOTE]  
>  No momento, este método não é compatível com [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Se você usar este método, o driver JDBC se lembrará da configuração, mas atualmente ele não age em função dela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *direction*  
  
 Um **int** que indica a direção de fetch sugerida. Pode ser um dos seguintes valores:  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setFetchDirection é especificado pelo método setFetchDirection na interface do resultset.  
  
 O valor inicial deste método é determinado pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que gerou este objeto SQLServerResultSet. A direção de busca pode ser alterada a qualquer momento.  
  
> [!NOTE]  
>  Usar este método quando o tipo de cursor é somente encaminhamento não tem nenhum efeito.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
