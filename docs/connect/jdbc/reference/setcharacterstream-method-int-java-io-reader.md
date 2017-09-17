---
title: "Método setCharacterStream (int, Java.IO. Reader) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8d4e1f7-14fc-4590-af98-1eda30d2ca6d
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 21519761d83e975a5c99dd2658b2031df2daf8df
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setcharacterstream-method-int-javaioreader"></a>Método setCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Java.IO. Reader especificado.  
  
> [!NOTE]  
>  Este recurso foi introduzido com o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver versão 2.0.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o número do parâmetro.  
  
 *leitor*  
  
 O objeto Java.IO. Reader que contém os dados Unicode.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface PreparedStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método setCharacterStream &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
