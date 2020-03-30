---
title: Método createBlob (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 630a93b0-6e3c-4255-a007-1097ce0ee243
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3d70c72b860044a7e61b4a6dc5474c465fb60e89
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67955394"
---
# <a name="createblob-method-sqlserverconnection"></a>Método createBlob (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto Blob sem dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Blob createBlob()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Blob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método createBlob é especificado pelo método createBlob na interface java.sql.Connection.  
  
 Esse método substitui a necessidade do [Construtor SQLServerBlob &#40;SQLServerConnection, byte&#41;](../../../connect/jdbc/reference/sqlserverblob-constructor-sqlserverconnection-byte.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
