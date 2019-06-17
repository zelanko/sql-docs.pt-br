---
title: Método getApplicationName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7396b679dce0e655ae6124b1198afc306151ac97
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798971"
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>Método getApplicationName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **cadeia de caracteres** que contém o nome do aplicativo ou "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]", se não houver valor definido.  
  
## <a name="remarks"></a>Remarks  
 O nome do aplicativo é usado para identificar o aplicativo específico em várias ferramentas de criação de perfil e log do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o nome do aplicativo não for definido, o método getApplicationName retornará a cadeia de caracteres não localizada "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
