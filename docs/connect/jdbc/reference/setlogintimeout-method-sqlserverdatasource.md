---
title: Método setLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83d6869075e296465ee9c60b0c5032407d4fe2da
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925760"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Método setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o número de segundos que este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) aguardará enquanto tenta estabelecer uma conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *loginTimeout*  
  
 Um valor **int** que representa o número de segundos de espera. Zero indica que o tempo limite é o padrão do sistema, especificado como 15 segundos por padrão.  
  
## <a name="remarks"></a>Comentários  
 Esse método setLoginTimeout é especificado pelo método setLoginTimeout na interface java.sql.DataSource.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
