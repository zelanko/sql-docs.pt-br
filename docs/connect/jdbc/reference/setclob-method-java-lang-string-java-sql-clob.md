---
title: Método setClob (java.lang.String, java.sql.Clob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 256b5f55-7a6d-44fb-9a09-19fa39f19c35
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a3f54f499504cede4c3cca2d87c20c095eda23
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925306"
---
# <a name="setclob-method-javalangstring-javasqlclob"></a>Método setClob (java.lang.String, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Clob especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.sql.Clob x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *parameterName*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *x*  
  
 Um objeto Clob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setClob é especificado pelo método setClob na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
