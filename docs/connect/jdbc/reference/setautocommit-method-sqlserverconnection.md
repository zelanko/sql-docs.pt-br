---
title: Método setAutoCommit (SQLServerConnection)
description: Conheça os detalhes da API pública para o método setAutoCommit na classe SQLServerConnection do JDBC Driver para SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117fa85e5ec6bdd7d0d37de9fc057dd8127cf42a
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435377"
---
# <a name="setautocommit-method-sqlserverconnection"></a>Método setAutoCommit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o modo de confirmação automática do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) como o estado fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *value*  
  
 **true** para habilitar e **false** para desabilitar o modo de confirmação automática da conexão.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setAutoCommit é especificado pelo método setAutoCommit na interface java.sql.Connection.  
  
 Se uma conexão estiver no modo de confirmação automática, todas as instruções SQL serão executadas e confirmadas como transações individuais. Caso contrário, suas instruções SQL serão agrupadas em transações que são terminadas por uma chamada aos métodos [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) ou [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md). Por padrão, as novas conexões ficam no modo de confirmação automática.  
  
 A confirmação ocorre quando a instrução é concluída ou a próxima execução ocorre, o que ocorrer primeiro. Quando as instruções retornarem um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md), a instrução será concluída quando a última linha do conjunto de resultados for recuperada ou quando o conjunto de resultados for fechado. Em casos avançados, uma única instrução pode retornar vários resultados além dos valores de parâmetro de saída. Nesses casos, a confirmação ocorrerá quando todos os resultados e valores de parâmetro de saída tiverem sido recuperados.  
  
 Quando o modo de confirmação automática for **false**, o JDBC Driver iniciará uma nova transação implicitamente depois de cada confirmação.  
  
> [!NOTE]  
> Se esse método for chamado durante uma transação, esta será confirmada.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)  
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
