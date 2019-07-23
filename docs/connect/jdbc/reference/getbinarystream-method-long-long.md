---
title: Método getBinaryStream (Long, Long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30bc8882-04b4-4efd-95e4-7d3a2a8c1d47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5cc12f9e7ed7a83363766355fa5d340a459a332b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953656"
---
# <a name="getbinarystream-method-long-long"></a>Método getBinaryStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um objeto de fluxo de entrada que contém um valor BLOB parcial usando a posição inicial e o comprimento especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.InputStream getBinaryStream(long pos, long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 O deslocamento para o primeiro byte do valor parcial ser recuperado.  
  
 *length*  
  
 O comprimento em bytes do valor parcial a ser recuperado.  
  
## <a name="return-value"></a>Valor retornado  
 Um fluxo de entrada que contém os dados do BLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getBinaryStream é especificado pelo método getBinaryStream na interface java. Sql. blob.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
