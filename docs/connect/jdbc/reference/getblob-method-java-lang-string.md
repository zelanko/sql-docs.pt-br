---
title: Método getBlob (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fe74b50-9ccd-4973-a93a-6da2c20a4154
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e023030d01459ef0f7be9b9c61e5f6b8ba1e4d14
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67953591"
---
# <a name="getblob-method-javalangstring"></a>Método getBlob (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro JDBC BLOB designado como um objeto Blob na linguagem de programação Java, considerando o nome do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Blob getBlob(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Blob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBlob é especificado pelo método getBlob na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBlob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
