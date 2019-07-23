---
title: Método getNCharacterStream (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f1cfa4e4-3e1f-4504-b0de-cc626d653661
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 004f5d89eaaa4293ae7da0058733b261c01c7531
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981689"
---
# <a name="getncharacterstream-method-int-sqlserverresultset"></a>Método getNCharacterStream (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto Reader.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getNCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto leitor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getNCharacterStream é especificado pelo método getNCharacterStream na interface java. Sql. ResultSet.  
  
 Esse método pode ser usado para recuperar o valor de uma coluna **nvarchar**, **nchar**, **nvarchar (max)** , **ntext** ou **xml** na linha atual deste objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Se você tentar usar esse método para recuperar valores de outros tipos de dados, uma exceção será lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getNCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
