---
title: Método updateNClob (java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a025d124-3634-49fa-8bb5-e9b98f2d5de3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ff1732e9ea7d146fdd129dc86030039afbf97444
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66776722"
---
# <a name="updatenclob-method-javalangstring-javasqlnclob"></a>Método updateNClob (java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **NClob**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.sql.NClob x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que indica o rótulo de coluna.  
  
 *x*  
  
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
  
  
