---
title: Método getScale (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e77c6dcfd46b6fbb522312738bd24c9f4ac94fe0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getscale-method-sqlserverparametermetadata"></a>Método getScale (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o número de dígitos à direita da vírgula decimal do parâmetro designado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getScale(int param)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *param*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Em **int** que indica a escala do parâmetro designado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getScale é especificado pelo método getScale na interface Java.SQL. parametermetadata.  
  
 Esse método obtém dígitos da coluna à direita da vírgula decimal. Para tipos que não têm uma vírgula decimal, esse método retorna "0".  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Membros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Classe SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
