---
title: Classe SQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f59867c195a333d0bd4bee7996d19fbeae156c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845881"
---
# <a name="sqlserverconnection-class"></a>Classe SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa uma conexão JDBC para um [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), Java.IO. Serializable  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerConnection oferece suporte ao pool de conexão JDBC e pode ser uma conexão JDBC física ou uma conexão JDBC lógica. SQLServerConnection gerencia o controle de transação para todas as instruções que foram criadas a partir dela e pode participar de transações distribuídas XA gerenciadas por um adaptador XAResource.  
  
 SQLServerConnection gerencia um pool de identificadores de instrução preparada. As instruções preparadas são preparadas uma vez e geralmente são executadas várias vezes com valores de dados diferentes para seus parâmetros. Elas também são mantidas entre encerramentos de conexão (em pool) lógica.  
  
> [!NOTE]  
>  SQLServerConnection não é thread-safe. No entanto, várias instruções que são criadas de uma única conexão podem ser processadas ao mesmo tempo em threads simultâneos.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerConnection, a interface Java.SQL. Connection e a interface ISQLServerConnection. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
