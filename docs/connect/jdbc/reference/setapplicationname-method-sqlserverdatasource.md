---
title: "Método setApplicationName (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dddba9b465d2b9bd2edfe42f850af6a3b64cd503
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
 Um **cadeia de caracteres** que contém o nome do aplicativo.  
  
## <a name="remarks"></a>Comentários  
 O nome do aplicativo é usado para identificar o aplicativo específico em várias [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] de criação de perfil e as ferramentas de log. Se o nome do aplicativo não for definido, o método getApplicationName retorna a cadeia de caracteres não localizada "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
