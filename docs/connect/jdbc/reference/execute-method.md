---
title: Método Execute () | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f7e87040fa74954435ed52f9923568e8bfed3fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954923"
---
# <a name="execute-method-"></a>Método execute ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL no objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que pode ser qualquer tipo de instrução SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean execute()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se a instrução retornar um conjunto de resultados. **false** se retornar uma contagem de atualização ou nenhum resultado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método é especificado pelo método execute na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método execute &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
