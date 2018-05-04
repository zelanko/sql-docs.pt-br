---
title: Método getAsciiStream (SQLServerNClob) | Microsoft Docs
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
ms.assetid: ff1d47e4-572a-4169-a631-ac261f7642b3
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1aa0fa0989d449f2c4ff21c7ce0cabe2a5fc2eb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getasciistream-method-sqlservernclob"></a>Método getAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o **NCLOB** valor designado por este **NClob** objeto como um fluxo ASCII.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto InputStream que contém os dados NCLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getAsciiStream é especificado pelo método na interface java.sql.SQLServerNClob getAsciiStream.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
