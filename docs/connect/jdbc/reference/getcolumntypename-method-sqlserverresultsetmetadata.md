---
title: Método getColumnTypeName (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnTypeName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a444da82-c1af-40a5-9774-02476416c92c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77135659d9c5b1b2580c4a5e8a382d4ef0914e6b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923386"
---
# <a name="getcolumntypename-method-sqlserverresultsetmetadata"></a>Método getColumnTypeName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o nome de tipo específico do banco de dados da coluna designada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getColumnTypeName(int column)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *column*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome do servidor para a coluna.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getColumnTypeName é especificado pelo método getColumnTypeName na interface java.sql.ResultSetMetaData.  
  
 O [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 tem alterações de comportamento na coluna TYPE_NAME. Consulte [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md) para saber mais.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
