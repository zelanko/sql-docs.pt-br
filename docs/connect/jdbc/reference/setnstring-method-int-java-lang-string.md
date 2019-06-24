---
title: Método setNString (int, lang) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b7da6d44-f5b1-44f8-95f5-40179968b1b0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56e07aec8b54eac95340c6997bdaa676e7cf0219
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800362"
---
# <a name="setnstring-method-int-javalangstring"></a>Método setNString (int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto **String** especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNString(int parameterIndex,  
                                                  java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *value*  
  
 Um objeto **String** que contém o valor do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deve ser usado para **NCHAR**, **NVARCHAR**, **NTEXT**, e **XML** tipos de dados.  
  
 Esse método setNString é especificado pelo método setNString na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
