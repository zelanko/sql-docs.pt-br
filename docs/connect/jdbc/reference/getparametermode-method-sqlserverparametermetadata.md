---
title: Método getParameterMode (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterMode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d93c9b70-18c2-44bb-a6de-70a7e940d806
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 74da1d6791756c9bd212b9f202a130d50a0c8b55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771484"
---
# <a name="getparametermode-method-sqlserverparametermetadata"></a>Método getParameterMode (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o modo do parâmetro designado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getParameterMode(int param)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *param*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o modo do parâmetro designado, que pode ser um dos seguintes valores:  
  
 ParameterMetaData.parameterModeIn  
  
 ParameterMetaData.parameterModeInOut  
  
 ParameterMetaData.parameterModeOut  
  
 ParameterMetaData.parameterModeUnknown  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getParameterMode é especificado pelo método getParameterMode na interface parametermetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membros SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
