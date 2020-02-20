---
title: Método setAutoCommit (SQLServerConnection) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbf9b18fdc6b590f085b5be6babd64100006163a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975266"
---
# <a name="setautocommit-method-sqlserverconnection"></a>Método setAutoCommit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o modo de confirmação automática do objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) como o estado fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *value*  
  
 **true** para habilitar o modo de confirmação automática para a conexão, **false** para desabilitá-lo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setAutoCommit é especificado pelo método setAutoCommit na interface java.sql.Connection.  
  
 Se uma conexão estiver no modo de confirmação automática, todas as suas instruções SQL serão executadas e confirmadas como transações individuais. Caso contrário, suas instruções SQL serão agrupadas em transações que são terminadas por uma chamada aos métodos [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) ou [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md). Por padrão, as novas conexões estão no modo de confirmação automática.  
  
 A confirmação ocorre quando a instrução é concluída ou a próxima execução ocorre, o que ocorrer primeiro. No caso de instruções que retornam um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md), a instrução será concluída quando a última linha do conjunto de resultados tiver sido recuperada ou quando o conjunto de resultados tiver sido fechado. Em casos avançados, uma única instrução pode retornar vários resultados além dos valores de parâmetro de saída. Nesses casos, a confirmação ocorrerá quando todos os resultados e valores de parâmetro de saída tiverem sido recuperados.  
  
 Quando o modo de confirmação automática for **false**, o JDBC Driver iniciará uma nova transação implicitamente depois de cada confirmação.  
  
> [!NOTE]  
>  Se esse método for chamado durante uma transação, esta será confirmada.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
