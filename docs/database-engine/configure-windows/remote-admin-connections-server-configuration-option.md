---
title: "Opção de configuração de servidor remote admin connections | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9cfa41a838ebb89777b44464ec2b2a48b256c3f9
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="remote-admin-connections-server-configuration-option"></a>Opção de configuração de servidor remote admin connections
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma DAC (conexão de administrador dedicada). A DAC permite que um administrador acesse um servidor em execução para desempenhar funções de diagnóstico ou executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , ou para solucionar problemas no servidor, mesmo quando o servidor está bloqueado ou está sendo executado em um estado anormal e não está respondendo a uma conexão com o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Por padrão, a DAC só está disponível a partir de um cliente no servidor. Para permitir que os aplicativos cliente de computadores remotos utilizem a DAC, use a opção remote admin connections sp_configure.  
  
 Por padrão, a DAC escuta apenas no endereço IP de loopback (127.0.0.1), porta 1434. Se a porta TCP 1434 não estiver disponível, uma porta TCP será atribuída dinamicamente quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for iniciado. Quando houver mais de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada em um computador, verifique o número da porta TCP no log de erros.  
  
 A tabela a seguir lista os possíveis valores para a opção remote admin connections.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Indica que apenas conexões locais são permitidas usando a DAC.|  
|1|Indica que são permitidas conexões remotas usando a DAC.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita a DAC a partir de um computador remoto.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  

