---
title: Método updateClob (int, Java.IO. Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df60fbf1-44b2-4658-84a5-5cb129ce2dc6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc352675eb43ea1c560ae7de0feea4749b9c7a07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updateclob-method-int-javaioreader"></a>Método updateClob (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada usando o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateClob(int columnIndex,  
                        java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *Leitor*  
  
 Um objeto do leitor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateClob é especificado pelo método updateClob na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
