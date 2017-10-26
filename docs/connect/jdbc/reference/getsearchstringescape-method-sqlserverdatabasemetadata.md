---
title: "Método getSearchStringEscape (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1008cd0fdec7aa60d9d66c62cfb08ad84ca1cd5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentários  
 Esse método getSearchStringEscape é especificado pelo método getSearchStringEscape na interface DatabaseMetadata.  
  
 Esse método é usado apenas para pesquisas de padrão de metadados. Ele retorna "\\". Um **cadeia de caracteres** padrão de pesquisa pode escapar caracteres curinga ("%" e "_") e fornecê-los como literais colocando uma barra invertida. Isso se traduz "\\%" em "[%]" e "\\\_" para "[\_]".  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

