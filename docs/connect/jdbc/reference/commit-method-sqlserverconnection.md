---
title: Método commit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50afbfa25052e0f602c486d011ce666a599372e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923583"
---
# <a name="commit-method-sqlserverconnection"></a>Método commit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Torna permanentes todas as alterações feitas desde a confirmação ou reversão anterior e libera todos os bloqueios de banco de dados atualmente mantidos pelo objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método commit é especificado pelo método commit na interface java.sql.Connection.  
  
 Esse método deverá ser usado apenas quando o modo de confirmação automática tiver sido desabilitado.  
  
 Observe que esse método irá falhar e lançar uma exceção se o cliente iniciar uma transação manual e, em seguida, por algum motivo o SQL Server reverterá a transação manual. Por exemplo, uma exceção será lançada se o cliente chamar um procedimento armazenado que explicitamente chama ROLLBACK TRANSACTION e, então, o cliente chamará o método commit. Além disso, se o SQL Server gerar um erro de severidade suficiente (16 ou mais alto) para reverter o cliente que iniciou a transação manual, uma chamada subsequente ao método commit lançará uma exceção.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
