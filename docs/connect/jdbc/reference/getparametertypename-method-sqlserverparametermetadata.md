---
title: Método getParameterTypeName (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterTypeName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebe7ff0f-3cc0-408e-9503-4ca754c9c37f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 17fc9ccf4b2483d00b2e6576d7e33441f6b90fb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771412"
---
# <a name="getparametertypename-method-sqlserverparametermetadata"></a>Método getParameterTypeName (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o nome do tipo específico de banco de dados do parâmetro designado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getParameterTypeName(int param)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *param*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome de tipo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getParameterTypeName é especificado pelo método getParameterTypeName na interface parametermetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membros SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
