---
title: Método getCatalogName (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getCatalogName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 64f62569-5d8e-411f-a98d-ddc52798391e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6282e994eff5b8b06ac59b97f6ef1223dd6172a7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921546"
---
# <a name="getcatalogname-method-sqlserverresultsetmetadata"></a>Método getCatalogName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtém o nome do catálogo da tabela que inclui a coluna designada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getCatalogName(int column)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *column*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome do catálogo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCatalogName é especificado pelo método getCatalogName da interface java.sql.ResultSetMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLServerResultSetMetaData Methods](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
