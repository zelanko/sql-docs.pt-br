---
title: Método setNClob (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a595679a-89b7-4b18-9ad2-d9cb13af2a28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 252d16871a3aa161eacab99a62eaf4f8a2f03ae8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973740"
---
# <a name="setnclob-method-javalangstring-javaioreader"></a>Método setNClob (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterName*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *reader*  
  
 Um objeto leitor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deve ser usado para tipos de dados de parâmetro **nchar**, **nvarchar**, **ntext**e **XML** .  
  
 Esse método setNClob é especificado pelo método setNClob na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
