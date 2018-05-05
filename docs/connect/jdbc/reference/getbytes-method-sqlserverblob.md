---
title: Método getBytes (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a872d042c0a96123cccffac5c5a6f8e2b686c4d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getbytes-method-sqlserverblob"></a>Método getBytes (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém os dados do BLOB como uma matriz de bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição inicial, iniciando em 1 (não em 0).  
  
 *Comprimento*  
  
 O comprimento dos dados a serem obtidos.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **bytes** matriz que contém os dados solicitados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBytes é especificado pelo método getBytes na interface Java.SQL.  
  
 Se você tiver um valor nulo ou ter comprimento zero BLOB e tentar obter exatamente zero bytes na posição 1, vazio **bytes** matriz é retornada (matriz de bytes de comprimento 0).  
  
 Se você tiver um BLOB de comprimento nulo ou zero e tentar obter qualquer comprimento de bytes em uma posição que não seja a 1, uma exceção de posição será lançada.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
