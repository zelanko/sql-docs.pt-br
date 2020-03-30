---
title: Método setSQLXML (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 70bbdde0-75f7-4169-88c5-dbbe2c4bcd03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b2a1af43238d2f0da19c65535f3c6f84fa0e434f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972804"
---
# <a name="setsqlxml-method-sqlserverpreparedstatement"></a>Método setSQLXML (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto SQLXML especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setSQLXML(int parameterIndex,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *xmlObject*  
  
 Um objeto SQLXML que contém o valor do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setSQLXML é especificado pelo método setSQLXML na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
