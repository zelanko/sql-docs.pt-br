---
title: Método de posição (Byte, Long) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf8cfa3bb6aed74c7689639698715dc24803d46d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976468"
---
# <a name="position-method-byte-long"></a>Método position (byte[], long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a posição de um padrão especificado no BLOB com base no padrão de matriz de **byte** fornecido e no índice inicial.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *bPattern*  
  
 O padrão a ser pesquisado.  
  
 *start*  
  
 O índice inicial no qual pesquisar.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **long** da posição em que o padrão foi localizado ou -1 se não foi localizado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método position é especificado pelo método position na interface java. Sql. blob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método &#40;de posição SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
