---
title: "Método getBytes (SQLServerBlob) | Microsoft Docs"
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
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f1139f0deb886265da6c7c56e682372155a0e3b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
 *length*  
  
 O comprimento dos dados a serem obtidos.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **bytes** matriz que contém os dados solicitados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBytes é especificado pelo método getBytes na interface Java.SQL.  
  
 Se você tiver um valor nulo ou ter comprimento zero BLOB e tentar obter exatamente zero bytes na posição 1, vazio **bytes** matriz é retornada (matriz de bytes de comprimento 0).  
  
 Se você tiver um BLOB de comprimento nulo ou zero e tentar obter qualquer comprimento de bytes em uma posição que não seja a 1, uma exceção de posição será lançada.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
