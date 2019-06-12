---
title: Método setAsciiStream (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6e1779df-3b2a-41d1-8dca-99692cc9da14
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 76d58f43e1caded32ac03e2c8f96ee5b9365bb72
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764974"
---
# <a name="setasciistream-method-sqlserverclob"></a>Método setAsciiStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um fluxo a ser usado para gravar caracteres ASCII no CLOB iniciando na posição determinada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no objeto CLOB.  
  
## <a name="return-value"></a>Valor retornado  
 O fluxo no qual os caracteres ASCII codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface do CLOB.  
  
 Os dados de caractere no CLOB são substituídos pelo fluxo de saída iniciando na posição determinada e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará os caracteres ASCII. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
