---
title: getCharacterStream (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getCharacterStream(String paramName)
apilocation:
- SQLServerCallableStatement.getCharacterStream(String paramName)
apitype: Assembly
ms.assetid: 5281e1b8-19b8-4fe5-83be-929d1987e25d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57b92b502aa940fb9aebca653856782ab1c6b2e1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924935"
---
# <a name="getcharacterstream-javalangstring"></a>getCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto java.io.Reader, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.io.Reader getCharacterStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *paramName*  
  
 Uma **String** que indica o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Reader.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método getCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
