---
title: Classe SQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a14627f54e1d297642cb2c555fb8427acb2da5a7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803085"
---
# <a name="sqlserverconnection-class"></a>Classe SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa uma conexão JDBC com um banco de dados do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Remarks  
 O SQLServerConnection é compatível com o pool de conexão JDBC e pode ser uma conexão JDBC física ou uma conexão JDBC lógica. O SQLServerConnection gerencia o controle de transações para todas as instruções que foram criadas dele e pode participar de transações distribuídas XA gerenciadas por meio de um adaptador XAResource.  
  
 SQLServerConnection gerencia um pool de identificadores de instrução preparada. As instruções preparadas são preparadas uma vez e geralmente são executadas várias vezes com valores de dados diferentes para seus parâmetros. Elas também são mantidas entre encerramentos de conexão (em pool) lógica.  
  
> [!NOTE]  
>  SQLServerConnection não é thread-safe. No entanto, várias instruções que são criadas de uma única conexão podem ser processadas ao mesmo tempo em threads simultâneos.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerConnection, interface Connection e interface ISQLServerConnection. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
