---
description: getAsciiStream (int)
title: getAsciiStream (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getAsciiStream(int paramIndex)
apilocation:
- SQLServerCallableStatement.getAsciiStream(int paramIndex)
apitype: Assembly
ms.assetid: 9d8b235e-4208-40ee-b5a5-bc76f73b82f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7db272ce8d8577b72c906062b9d95f4b58479306
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437438"
---
# <a name="getasciistream-int"></a>getAsciiStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um fluxo de caracteres **ASCII**, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.io.InputStream getAsciiStream(int paramIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *paramIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método getAsciiStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
