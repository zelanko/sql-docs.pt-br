---
title: Método updateNClob (int, NCLOB) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6e9bca18-f64e-46a4-8541-2c9c39b393b5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 15c64b062cd0da35a8f1c870da60062620b9e30a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798406"
---
# <a name="updatenclob-method-int-javasqlnclob"></a>Método updateNClob (int, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **NClob**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateNClob(int columnIndex,  
                        java.sql.NClob nClob)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
 *nClob*  
  
 Um objeto NClob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateNClob é especificado pelo método updateNClob na interface java.sql.ResultSet.  
  
 Esse método tem suporte apenas no **nvarchar (max)** , **ntext**, e **xml** colunas. Seu uso em quaisquer outros tipos de dados fará com que uma exceção seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateNClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
