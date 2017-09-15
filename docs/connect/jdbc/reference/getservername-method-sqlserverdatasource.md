---
title: "Método getServerName (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f7c77c52a62465eea584e3fa695810a65ffc202
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getservername-method-sqlserverdatasource"></a>Método getServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o nome do servidor ou nulo se nenhum valor for definido.  
  
## <a name="remarks"></a>Comentários  
 O nome do servidor é o nome de host do computador de destino que está executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Se a propriedade getServerName não está definida, getServerName retornará o valor padrão de null.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
