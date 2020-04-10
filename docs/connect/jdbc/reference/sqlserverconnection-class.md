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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6248e126806b15592bbc3d6c458045ca7d9db042
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920673"
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
  
## <a name="remarks"></a>Comentários  
 O SQLServerConnection é compatível com o pool de conexão JDBC e pode ser uma conexão JDBC física ou uma conexão JDBC lógica. O SQLServerConnection gerencia o controle de transações para todas as instruções que foram criadas dele e pode participar de transações distribuídas XA gerenciadas por meio de um adaptador XAResource.  
  
 A SQLServerConnection gerencia um pool de identificadores de instrução preparada. As instruções preparadas são preparadas uma vez e geralmente são executadas várias vezes com valores de dados diferentes para seus parâmetros. Elas também são mantidas entre encerramentos de conexão (em pool) lógica.  
  
> [!NOTE]  
>  A SQLServerConnection não é thread-safe. No entanto, várias instruções que são criadas de uma única conexão podem ser processadas ao mesmo tempo em threads simultâneos.  
  
 Essa classe dá suporte ao desencapsulamento da classe SQLServerConnection, da interface java.sql.connection e da interface ISQLServerConnection. Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
