---
title: Método updateNString (Java, Java) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6daca03f-c60f-4842-b9e3-11d136e78312
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41c12f32b1b42153baa79543ca284872040763ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850121"
---
# <a name="updatenstring-method-javalangstring-javalangstring"></a>Método updateNString (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **cadeia de caracteres** valor usando o rótulo da coluna especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateNString(java.lang.String columnLabel,  
                          java.lang.String nString)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Um **cadeia de caracteres** que contém o rótulo da coluna.  
  
 *nString*  
  
 Um **cadeia de caracteres** objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateNString é especificado pelo método updateNString na interface Java.SQL. resultset.  
  
 Esse método passa a Java **cadeia de caracteres** marcada **nchar**, **nvarchar (max)**, **ntext**, e **xml** colunas. O uso em outras colunas de tipo de dados lançará uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateNString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
