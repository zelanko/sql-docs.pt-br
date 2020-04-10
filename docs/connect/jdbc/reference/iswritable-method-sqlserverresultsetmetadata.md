---
title: Método isWritable (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isWritable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 50846aa8-e4e5-4fc3-a638-0e5fa8b597be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f199ae0fea034ed83e0b633939b2224e531e9f8c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80915044"
---
# <a name="iswritable-method-sqlserverresultsetmetadata"></a>Método isWritable (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se é possível que uma gravação na coluna designada seja bem-sucedida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isWritable(int column)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *column*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se as gravações forem bem-sucedidos na coluna. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método isWritable é especificado pelo método isWritable na interface java.sql.ResultSetMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLServerResultSetMetaData Methods](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
