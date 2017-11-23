---
title: "Método setAsciiStream (SQLServerNClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b49fd4f18538c1a42a7822f60a090d539e52c4e8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setasciistream-method-sqlservernclob"></a>Método setAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um fluxo a ser usado para gravar ASCII caracteres para o **NCLOB** valor que este **Java.SQL. NCLOB** objeto representa, começando na posição especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição na qual iniciar a gravação de **NCLOB** objeto; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto OutputStream que representa o fluxo ao qual os caracteres ASCII codificados pode ser gravado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface Java.SQL. NCLOB.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
