---
title: Método getCharacterStream (long, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2881f3a9e0d3a4179334256aa7d2917917cf97f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66781324"
---
# <a name="getcharacterstream-method-long-long"></a>Método getCharacterStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna os dados de **Clob** como um objeto Reader ou como um fluxo de caracteres com a posição e o comprimento especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 Um **long** que indica o deslocamento do primeiro caractere do valor parcial a ser recuperado.  
  
 *length*  
  
 Um **long** que indica o comprimento, em caracteres, do valor parcial a ser recuperado.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Reader que contém os dados **Clob**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface do CLOB.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getCharacterStream &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  
