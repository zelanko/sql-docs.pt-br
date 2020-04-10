---
title: Membros de SQLServerParameterMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6255e854bd7c6a9d5d8dca99a4b702ad7e0bbce
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923506"
---
# <a name="sqlserverparametermetadata-members"></a>Membros de SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  As tabelas a seguir listam os membros expostos pela classe [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md).  
  
## <a name="constructors"></a>Construtores  
 Nenhum.  
  
## <a name="fields"></a>Campos  
 Nenhum.  
  
## <a name="inherited-fields"></a>Campos herdados  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn, parameterModeInOut, parameterModeOut, parameterModeUnknown, parameterNoNulls, parameterNullable, parameterNullableUnknown|  
  
## <a name="methods"></a>Métodos  
  
|Nome|DESCRIÇÃO|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|Recupera o nome totalmente qualificado da classe Java cujas instâncias devem ser passadas para o método [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) da classe [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|Recupera o número de parâmetros no objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) para o qual esse objeto [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) contém informações.|  
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
  
## <a name="see-also"></a>Consulte Também  
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
