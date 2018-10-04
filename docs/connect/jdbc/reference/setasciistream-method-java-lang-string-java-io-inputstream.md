---
title: Método para o fluxo de entrada setAsciiStream | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45d76d8dc1123cf17d95a0e6587b79168bedefb0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643944"
---
# <a name="setasciistream-method-javalangstring-javaioinputstream"></a>Método setAsciiStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o fluxo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterName*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *x*  
  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface do PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [setAsciiStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
