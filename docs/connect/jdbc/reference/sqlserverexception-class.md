---
title: Classe SQLServerException | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd894bf23d8b1643722691451ccf3ae29ec6cd54
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverexception-class"></a>Classe SQLServerException
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa uma execução malsucedida ou incompleta de uma instrução SQL.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** SqlException  
  
 **Implementa:** Java.IO. Serializable  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>Comentários  
 A classe SQLServerException manipula códigos de estado SQL 92 e XOPEN. Eles podem ser trocados usando uma propriedade de conexão especificada pelo usuário. As exceções são gravadas em qualquer arquivo de log aberto que foi especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

