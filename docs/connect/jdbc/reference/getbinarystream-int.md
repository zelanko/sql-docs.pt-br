---
title: getBinaryStream (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBinaryStream(int paramIndex)
apilocation:
- SQLServerCallableStatement.getBinaryStream(int paramIndex)
apitype: Assembly
ms.assetid: a766818e-cd05-4a07-a1ae-88966017448c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a7fb65620f619f0bd6f83208be707cd165e4b58
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920546"
---
# <a name="getbinarystream-int"></a>getBinaryStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um fluxo binário de bytes ininterruptos, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.io.InputStream getBinaryStream(int paramIndex)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *paramIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
