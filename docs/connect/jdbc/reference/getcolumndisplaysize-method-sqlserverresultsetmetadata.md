---
title: Método getColumnDisplaySize (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.getColumnDisplaySize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 21c25443-bd2b-4b60-9798-4efe2c158952
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 97d5899370329d49d6ed289e8742ebcab6d402d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832161"
---
# <a name="getcolumndisplaysize-method-sqlserverresultsetmetadata"></a>Método getColumnDisplaySize (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a largura máxima normal, em caracteres, para a coluna designada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getColumnDisplaySize(int column)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *column*  
  
 Um **int** que indica o índice da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que indica a largura máxima. Se a largura não for conhecida, retornará 0.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getColumnDisplaySize é especificado pelo método getColumnDisplaySize na interface Java.SQL. resultsetmetadata.  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] O JDBC Driver 3.0 possui alterações de comportamento na coluna COLUMN_SIZE. Consulte [Getcolumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
