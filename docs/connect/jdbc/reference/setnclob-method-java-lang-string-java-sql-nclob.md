---
title: Método setNClob (java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 41a768a7225b07af0a7238afa5ebbcfaf46365d6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800393"
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>Método setNClob (java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto NClob especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterName*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *value*  
  
 Um objeto NClob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deve ser usado para **NCHAR**, **NVARCHAR**, **NTEXT**, e **XML** tipos de dados do parâmetro.  
  
 Esse método setNClob é especificado pelo método setNClob na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
