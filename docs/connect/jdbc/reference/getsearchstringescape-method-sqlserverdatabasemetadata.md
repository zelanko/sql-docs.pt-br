---
title: Método getSearchStringEscape (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0eb3fd98c42615dba674e31ed2007fbcfc22f4ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>Método getSearchStringEscape (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o **cadeia de caracteres** que pode ser usado para substituir caracteres curinga.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o caractere curinga cadeia de caracteres de escape.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getSearchStringEscape é especificado pelo método getSearchStringEscape na interface DatabaseMetadata.  
  
 Esse método é usado apenas para pesquisas de padrão de metadados. Ele retorna "\\". Um **cadeia de caracteres** padrão de pesquisa pode escapar caracteres curinga ("%" e "_") e fornecê-los como literais colocando uma barra invertida. Isso se traduz "\\%" em "[%]" e "\\\_" para "[\_]".  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
