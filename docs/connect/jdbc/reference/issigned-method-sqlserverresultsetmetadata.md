---
title: Método isSigned (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isSigned
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d16672f-1515-4255-8b20-e7911c999f60
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fec14aa519dfcc5539005321f0110c25146ce6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796344"
---
# <a name="issigned-method-sqlserverresultsetmetadata"></a>Método isSigned (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se os valores da coluna designada são números com sinal.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isSigned(int column)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *column*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 **True** se a coluna contiver números com sinal. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método isSigned é especificado pelo método isSigned na interface do resultsetmetadata.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLServerResultSetMetaData Methods](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
