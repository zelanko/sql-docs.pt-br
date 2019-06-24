---
title: Método updateBlob (java.lang.String, java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 40f75549-5d5a-4de3-a271-4b8f0dd7b124
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1512bb2d20c62e30a1b35abde333abf14e595bdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787202"
---
# <a name="updateblob-method-javalangstring-javaioinputstream-long"></a>Método updateBlob (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada usando o fluxo de entrada especificado, que terá o número de bytes especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
                                              long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que contém o rótulo da coluna.  
  
 *inputStream*  
  
 Um objeto InputStream.  
  
 *length*  
  
 Um **long** que indica o comprimento do fluxo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateBlob é especificado pelo método updateBlob na interface do resultset.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateBlob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
