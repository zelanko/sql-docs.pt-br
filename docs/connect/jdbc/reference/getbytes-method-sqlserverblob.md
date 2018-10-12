---
title: Método getBytes (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 098937df965d9573701657ef6c2ec580de09daf3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729734"
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
  
## <a name="return-value"></a>Valor retornado  
 Uma matriz **byte** que contém os dados solicitados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBytes é especificado pelo método getBytes na interface Java.  
  
 Se você tiver um BLOB de comprimento nulo ou zero e tentar obter exatamente zero bytes na posição 1, uma matriz **byte** vazia será retornada (matriz de bytes de comprimento 0).  
  
 Se você tiver um BLOB de comprimento nulo ou zero e tentar obter qualquer comprimento de bytes em uma posição que não seja a 1, uma exceção de posição será lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
