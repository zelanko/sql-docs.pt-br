---
title: Método (Java.SQL. NCLOB, long) Position | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f2354278-d128-4cf4-a170-22c05fcb763b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21299de3fa9eb6a8c9d02691c2cdfc326de68765
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="position-method-javasqlnclob-long"></a>Método position (java.sql.NClob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a posição do caractere em que o especificado **NClob** objeto *searchstr* aparece nesta **NClob** objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
long position(java.sql.NClob searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *searchstr*  
  
 Um objeto NClob para pesquisa.  
  
 *Início*  
  
 A posição em que a pesquisa deve ser iniciada; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor de retorno  
 A posição em que a subcadeia de caracteres aparece; ou -1 se ela não estiver presente. A primeira posição é 1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método de posição é especificado pelo método na interface Java.SQL. NCLOB posição.  
  
## <a name="see-also"></a>Consulte também  
 [Método Position &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
