---
title: Método getMaxCharLiteralLength (SQLServerDatabaseMetaData) | Microsoft Docs
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
apiname:
- SQLServerDatabaseMetaData.getMaxCharLiteralLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 44e6e9df-4724-4c86-bbd2-ca750c248333
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46cf70ec4cb5787cc7456e5930d00b1f75a12c50
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getmaxcharliterallength-method-sqlserverdatabasemetadata"></a>Método getMaxCharLiteralLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número máximo de caracteres que o banco de dados em questão permite para uma literal de caractere.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getMaxCharLiteralLength()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica o número máximo de caracteres permitidos.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMaxCharLiteralLength é especificado pelo método getMaxCharLiteralLength na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
