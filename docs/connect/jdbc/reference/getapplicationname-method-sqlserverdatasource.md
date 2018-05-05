---
title: Método getApplicationName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0239d7d251b4104000646a8f98a3cae0be656853
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>Método getApplicationName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o nome do aplicativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o nome do aplicativo ou "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" se nenhum valor for definido.  
  
## <a name="remarks"></a>Remarks  
 O nome do aplicativo é usado para identificar o aplicativo específico em várias [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] de criação de perfil e as ferramentas de log. Se o nome do aplicativo não for definido, o método getApplicationName retorna a cadeia de caracteres não localizada "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
