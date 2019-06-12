---
title: Método setApplicationName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f4c4707e06b25e1bb9e394c141f5fb1afa90599
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765331"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>Método setApplicationName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *applicationName*  
  
 Uma **String** que contém o nome do aplicativo.  
  
## <a name="remarks"></a>Remarks  
 O nome do aplicativo é usado para identificar o aplicativo específico em várias ferramentas de criação de perfil e log do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o nome do aplicativo não for definido, o método getApplicationName retornará a cadeia de caracteres não localizada "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
