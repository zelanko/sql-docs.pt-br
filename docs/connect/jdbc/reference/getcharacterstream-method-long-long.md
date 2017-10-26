---
title: "Método getCharacterStream (long, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba910c36ff82209a668ef6d96987330705703080
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-long-long"></a>Método getCharacterStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o **Clob** como um objeto do leitor ou como um fluxo de caracteres com a posição especificada e o comprimento de dados.  
  
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
 Um objeto do leitor que contém o **Clob** dados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getCharacterStream é especificado pelo método getCharacterStream na interface do CLOB.  
  
## <a name="see-also"></a>Consulte também  
 [Método getCharacterStream &#40; SQLServerClob &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  

