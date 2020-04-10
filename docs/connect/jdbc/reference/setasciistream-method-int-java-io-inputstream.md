---
title: Método setAsciiStream (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02c2443d-44e1-4f16-a0d5-08d197838214
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af25d40d7b216d027a22474846323d8aeecadb70
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920162"
---
# <a name="setasciistream-method-int-javaioinputstream"></a>Método setAsciiStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número do parâmetro designado como o objeto java.io.InputStream fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto java.io.InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setAsciiStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
