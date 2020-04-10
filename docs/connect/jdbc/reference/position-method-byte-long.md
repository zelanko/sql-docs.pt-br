---
title: Método position (byte[], long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938254b8076d78ebd1ac768d130904077828aa03
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914382"
---
# <a name="position-method-byte-long"></a>Método position (byte[], long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a posição de um padrão especificado no BLOB com base no padrão de matriz de **byte** fornecido e no índice inicial.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *bPattern*  
  
 O padrão a ser pesquisado.  
  
 *start*  
  
 O índice inicial no qual pesquisar.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **long** da posição em que o padrão foi localizado ou -1 se não foi localizado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método position é especificado pelo método position na interface java.sql.Blob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método position &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
