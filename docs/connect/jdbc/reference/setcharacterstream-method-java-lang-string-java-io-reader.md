---
title: Método setCharacterStream (Java, Java.IO. Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 43acac5b-5a8a-4685-bee6-7194d2d03a52
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 735877f38cca2d6a5ce43f12b2e3ee347bc9b7c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-javalangstring-javaioreader"></a>Método setCharacterStream (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName,  
                                             java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nome do parâmetro*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *Leitor*  
  
 Um objeto do leitor que contém os dados Unicode.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método setCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
