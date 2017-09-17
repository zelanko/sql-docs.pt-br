---
title: "Método setClob (int, Java.IO. Reader, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 157882dd-1a96-4501-a895-46e88a49266e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ab3cc5c9342b1e115a73d6616d9fe99992c4a869
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setclob-method-int-javaioreader-long"></a>Método setClob (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado, o que é o número especificado de caracteres de comprimento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.io.Reader reader,  
                          long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *leitor*  
  
 Um objeto do leitor.  
  
 *length*  
  
 Um **longo** que indica o número de caracteres no valor do parâmetro.  
  
## <a name="remarks"></a>Comentários  
 Esse método setClob é especificado pelo método na interface PreparedStatement setClob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método setClob &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
