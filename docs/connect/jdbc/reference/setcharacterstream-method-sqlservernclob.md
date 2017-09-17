---
title: "Método setCharacterStream (SQLServerNClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 09042ee9-dfb1-4d0b-82bd-d1224b0aea80
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54ea45119a144852daff92dac5037b6f7407d259
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setcharacterstream-method-sqlservernclob"></a>Método setCharacterStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um fluxo a ser usado para gravar um fluxo de caracteres Unicode para a **NCLOB** valor que este **Java.SQL. NCLOB** objeto representa, começando na posição especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição na qual iniciar a gravação de **NCLOB** valor; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de gravador que representa o fluxo ao qual os caracteres Unicode codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface Java.SQL. NCLOB.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
