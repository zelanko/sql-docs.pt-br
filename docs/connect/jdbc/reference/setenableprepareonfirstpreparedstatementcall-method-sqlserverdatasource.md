---
title: Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c6c76715f45521c3cbaea37a89020c6cad27b5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693984"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>Método setEnablePrepareOnFirstPreparedStatementCall (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Especifica o comportamento para uma instância de conexão específica. Se essa configuração for false, a primeira execução de uma instrução preparada chamará sp_executesql e não prepara uma instrução, depois que a segunda execução acontece, ele chamará o sp_prepexec e configurar, na verdade, um identificador de instrução preparada. Execuções a seguir chamará sp_execute. Isso alivia a necessidade de sp_unprepare na instrução preparada fechar se a instrução é executada apenas uma vez.  
## <a name="syntax"></a>Sintaxe  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 O novo valor de **enablePrepareOnFirstPreparedStatementCall** propriedade de conexão.  

## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 Esse método está disponível na versão do JDBC driver 6.4 e daí.
 
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
