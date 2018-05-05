---
title: Método isNullable (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.sNullable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d7e07cff-6fc4-4c9c-8e8f-838c77734bc5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6461fc7627e752844f44839b3053bcfa56137d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="isnullable-method-sqlserverparametermetadata"></a>Método isNullable (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se os valores nulos são permitidos no parâmetro designado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int isNullable(int param)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *param*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica a nulidade do parâmetro designado, que pode ser um dos seguintes valores:  
  
 ParameterMetaData.parameterNoNulls  
  
 ParameterMetaData.parameterNullable  
  
 ParameterMetaData.parameterNullabilityUnknown  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isNullable é especificado pelo método isNullable na interface Java.SQL. parametermetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
