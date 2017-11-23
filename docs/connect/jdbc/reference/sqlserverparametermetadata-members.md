---
title: Membros de SQLServerParameterMetaData | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a08e8540e387cf9b7bc5d75b9e98bbb8bbf1a27
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverparametermetadata-members"></a>Membros de SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pelo [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) classe.  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Nome|Description|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn, parameterModeInOut, parameterModeOut, parameterModeUnknown, parameterNoNulls, parameterNullable, parameterNullableUnknown|  
  
## <a name="methods"></a>Métodos  
  
|Nome|Description|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|Recupera o nome totalmente qualificado da classe Java cujas instâncias devem ser passadas para o [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) método o [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|Recupera o número de parâmetros no [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) objeto para o qual o [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) objeto contém informações.|  
|[getParameterMode](../../../connect/jdbc/reference/getparametermode-method-sqlserverparametermetadata.md)|Recupera o modo do parâmetro designado.|  
|[getParameterType](../../../connect/jdbc/reference/getparametertype-method-sqlserverparametermetadata.md)|Recupera o tipo SQL do parâmetro designado.|  
|[getParameterTypeName](../../../connect/jdbc/reference/getparametertypename-method-sqlserverparametermetadata.md)|Recupera o nome do tipo específico de banco de dados do parâmetro designado.|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverparametermetadata.md)|Recupera o número de casas decimais do parâmetro designado.|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverparametermetadata.md)|Recupera o número de dígitos à direita da vírgula decimal do parâmetro designado.|  
|[isNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverparametermetadata.md)|Recupera se os valores nulos são permitidos no parâmetro designado.|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverparametermetadata.md)|Recupera se os valores do parâmetro designado podem ser números assinados.|  
  
## <a name="inherited-methods"></a>Métodos herdados  
  
|Classe herdada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Consulte também  
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
