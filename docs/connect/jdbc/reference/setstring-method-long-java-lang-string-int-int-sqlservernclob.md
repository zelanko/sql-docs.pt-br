---
title: Método setString (long, java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2d5e9f50-15b2-4c76-8bfc-3b5be49c2781
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ad49b4a5e675d4ff6635583e0b64a1e57434ff22
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762267"
---
# <a name="setstring-method-long-javalangstring-int-int-sqlservernclob"></a>Método setString (long, java.lang.String, int, int) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava a cadeia de caracteres especificada no NCLOB começando na posição especificada, com base no deslocamento e no comprimento especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int setString(long pos,  
              java.lang.String str,  
              int offset,  
              int len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no **NCLOB**; a primeira posição é 1.  
  
 *str*  
  
 A String a ser gravada no **NCLOB**.  
  
 *offset*  
  
 O deslocamento para *str*, para iniciar a leitura dos caracteres a serem gravados.  
  
 *len*  
  
 O número de caracteres a serem gravados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setString é especificado pelo método setString na interface java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
