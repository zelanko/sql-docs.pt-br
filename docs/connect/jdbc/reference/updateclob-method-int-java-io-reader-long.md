---
title: Método updateClob (int, Java.IO. Reader, long) | Microsoft Docs
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
ms.topic: article
ms.assetid: 5c958ccb-386a-4dd5-901d-5a106dac2683
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aec641b10888f2b3d57c4cd66e18cf63d3f43806
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="updateclob-method-int-javaioreader-long"></a>Método updateClob (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada usando o objeto Reader especificado, cujo tamanho tem um número de caracteres especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateClob(int columnIndex,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *Leitor*  
  
 Um objeto do leitor.  
  
 *Comprimento*  
  
 O número de caracteres nos dados do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateClob é especificado pelo método updateClob na interface Java.SQL. resultset.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
