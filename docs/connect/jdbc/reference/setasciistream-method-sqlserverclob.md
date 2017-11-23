---
title: "Método setAsciiStream (SQLServerClob) | Microsoft Docs"
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
apiname: SQLServerClob.setAsciiStream
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6e1779df-3b2a-41d1-8dca-99692cc9da14
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f501c9c610319e0cad34dfabfe70dbf3f6cfffe2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setasciistream-method-sqlserverclob"></a>Método setAsciiStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um fluxo a ser usado para gravar caracteres ASCII no CLOB iniciando na posição determinada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição em que a gravação deve ser iniciada no objeto CLOB.  
  
## <a name="return-value"></a>Valor de retorno  
 O fluxo no qual os caracteres ASCII codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface do CLOB.  
  
 Os dados de caractere no CLOB são substituídos pelo fluxo de saída iniciando na posição determinada e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará os caracteres ASCII. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
