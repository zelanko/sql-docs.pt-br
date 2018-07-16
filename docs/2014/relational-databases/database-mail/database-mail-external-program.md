---
title: Programa externo do Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc14bf4c5128cff5e836c894dbcd74aa8e7a5cc0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233346"
---
# <a name="database-mail-external-program"></a>Programa externo do Database Mail
  O executável externo do Database Mail é **DatabaseMail.exe**, que está localizado no **diretório MSSQL\Binn** da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O Database Mail usa a ativação do Service Broker para iniciar o programa externo quando há mensagens de email a serem processadas. O Database Mail inicia uma instância do programa externo. O programa externo é executado no contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Neste tópico:**  
  
-   [Conceitos de programas externos do Database Mail](#ComponentsAndConcepts)  
  
-   [Tarefas relacionadas para configurar programa externo do Database Mail](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Conceitos de programas externos do Database Mail  
 Ao ser iniciado, o programa externo se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando autenticação do Windows e começa a processar mensagens de email. Quando não há nenhuma mensagem a enviar no tempo limite especificado, o programa é encerrado. Você pode configurar o tempo que o programa deve aguardar antes de encerrar, usando o Assistente para Configuração do Database Mail ou procedimentos armazenados do Database Mail. Para obter mais informações, veja [sysmail_configure_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql).  
  
 O programa externo armazena informações em tabelas do sistema no banco de dados **msdb** . Se o programa externo não puder se comunicar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele registrará erros no log de eventos de aplicativos do Microsoft Windows. Há ainda outros registros de mensagens quando o nível de log é definido como **Detalhado** na caixa de diálogo **Configurar Parâmetros do Sistema** do **Assistente para Configuração do Database Mail**.  
  
 Observe que, por questão de eficiência, o programa externo coloca em cache as informações de conta e perfil. Portanto, alterações na configuração de contas e perfis podem não se refletir no programa externo por alguns minutos.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas para configurar programa externo do Database Mail  
  
|Tarefa de configuração|Link do tópico|  
|------------------------|----------------|  
|Especifique a hora do Programa Externo antes de sair.|[sysmail_configure_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql)|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Registro em log e auditoria do Database Mail](database-mail-log-and-audits.md)   
 [Database Mail](database-mail.md)  
  
  
