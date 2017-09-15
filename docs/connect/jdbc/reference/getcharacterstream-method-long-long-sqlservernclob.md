---
title: "Método getCharacterStream (long, long) (SQLServerNClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5a8028bc-c877-4668-b662-0746d462040e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e4777f2a081678a61ed8f00abbcd30f53a583cab
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-long-long-sqlservernclob"></a>Método getCharacterStream (long, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o **NCLOB** dados como um **leitor** objeto ou como um fluxo de caracteres com tamanho e a posição especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                  long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 Um **longo** que indica o deslocamento para o primeiro caractere do valor parcial a ser recuperado.  
  
 *length*  
  
 Um **longo** que indica o comprimento em caracteres do valor parcial a ser recuperado.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto do leitor que contém o **NCLOB** dados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface Java.SQL. NCLOB.  
  
## <a name="see-also"></a>Consulte também  
 [Método getCharacterStream &#40; SQLServerNClob &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
