---
title: Método (int, int) supportsConvert | Microsoft Docs
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
- SQLServerDatabaseMetaData.supportsConvert (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 54741cfd-32ac-46c5-8b09-fd60fd8833d7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d482ebf9a5baba07e72f9d9f2bbb446bd3378363
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supportsconvert-method-int-int"></a>Método supportsConvert (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte à função CONVERT para dois tipos de SQL fornecidos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsConvert(int fromType,  
                               int toType)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *fromType*  
  
 O tipo do JDBC do qual converter.  
  
 *toType*  
  
 O tipo do JDBC para o qual converter.  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método supportsConvert é especificado pelo método supportsConvert na interface DatabaseMetadata.  
  
## <a name="see-also"></a>Consulte também  
 [Método supportsConvert &#40;SQLServerDatabaseMetaData&#41;](../../../connect/jdbc/reference/supportsconvert-method-sqlserverdatabasemetadata.md)   
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
