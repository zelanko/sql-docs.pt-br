---
title: Método getServerName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3004ed22-5d69-4dd0-8761-d39f0b7dde13
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 487d214dbdd6974442749dd0cff6ac24fe9d1977
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979957"
---
# <a name="getservername-method-sqlserverdatasource"></a>Método getServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome da instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getServerName()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém o nome do servidor ou o valor nulo no caso de nenhum valor ter sido definido.  
  
## <a name="remarks"></a>Remarks  
 O nome do servidor é o nome do host do computador de destino que executa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se a propriedade getServerName não for definida, getServerName retornará o valor padrão de nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
