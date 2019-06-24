---
title: Método getNClob (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b95a22911f1b7e49f6310e9c06a7ea4ef4a899fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66784458"
---
# <a name="getnclob-method-javalangstring"></a>Método getNClob (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor de um parâmetro **NCLOB** do JDBC como um objeto NClob na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterName*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 ANClobobject.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getNClob é especificado pelo método getNClob na interface java.sql.CallableStatement.  
  
 Esse método dá suporte apenas à recuperação **NCHAR**, **NVARCHAR**, **NTEXT**, e **XML** parâmetros. Chamar esses métodos em outros parâmetros de tipo de dados causará uma exceção.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
