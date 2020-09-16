---
description: Método execute ()
title: Método execute () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.execute ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fa96d0f8-101b-422f-a767-405be9a5f74f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b0dbd5155fcd8dd00b534506ef0eff7a7aad8f8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437738"
---
# <a name="execute-method-"></a>Método execute ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL no objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que pode ser qualquer tipo de instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean execute()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true ** se a instrução retornar como um conjunto de resultados. **false** se ela retornar uma contagem de atualizações ou nenhum resultado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método é especificado pelo método execute na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método execute &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
