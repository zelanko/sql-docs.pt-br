---
title: "Método setBinaryStream (SQLServerBlob) | Microsoft Docs"
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
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 630244ef25c3206d9c66ad2797d1a435661d1a60
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setbinarystream-method-sqlserverblob"></a>Método setBinaryStream (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um fluxo que pode ser usado para gravar no valor do BLOB.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição em que a gravação deve ser iniciada no valor BLOB)  
  
## <a name="return-value"></a>Valor de retorno  
 Um fluxo de saída.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setBinaryStream é especificado pelo método setBinaryStream na interface Java.SQL.  
  
 Os dados no BLOB são substituídos pelo fluxo de saída iniciando na posição especificada e podem ultrapassar o comprimento inicial do BLOB. A especificação de um valor posição+1 acrescentará bytes. A transmissão de um valor posição+2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
