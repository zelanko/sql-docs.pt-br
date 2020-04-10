---
title: getBinaryStream (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBinaryStream(String paramName)
apilocation:
- SQLServerCallableStatement.getBinaryStream(String paramName)
apitype: Assembly
ms.assetid: 17f1ea5d-47f8-4a66-a0fc-d6554b8e3866
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cff11261836dd26b73cd1f0bb96c05d57c065e95
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920522"
---
# <a name="getbinarystream-javalangstring"></a>getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um fluxo binário de bytes ininterruptos, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.io.InputStream getBinaryStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *paramName*  
  
 Uma **String** que indica o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
