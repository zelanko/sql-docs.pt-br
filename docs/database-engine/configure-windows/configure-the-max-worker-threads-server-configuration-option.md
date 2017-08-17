---
title: "Configurar a opção de configuração de servidor max worker threads | Microsoft Docs"
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
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0fb31141506ab6391c25afde71e1433935e32718
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>Configurar a opção max worker threads de configuração de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **max worker threads** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **max worker threads** configura o número de threads de trabalho que estão disponíveis para os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os serviços de thread nativos dos sistemas operacionais de forma que um ou mais threads ofereçam suporte a cada rede à qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte simultaneamente, outro thread controle pontos de verificação de banco de dados e um pool de threads controle todos os usuários. O valor padrão de **max worker threads** é 0. Isso habilita o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a configurar automaticamente o número de threads de trabalho na inicialização. A configuração padrão é a melhor para a maioria dos sistemas. No entanto, dependendo de sua configuração de sistema, a definição de **max worker threads** com um valor específico às vezes melhora o desempenho.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção max worker threads, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção max worker threads](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Quando o número real de solicitações de consulta é menor que a quantidade definida em **max worker threads**, um thread controla cada solicitação de consulta. Porém, se o número real de solicitação de consulta exceder a quantia definida em **max worker threads**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará o pool dos threads de trabalho de forma que próximo thread de trabalho disponível possa controlar a solicitação.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O thread pooling ajuda a otimizar o desempenho quando são conectados grandes números de clientes ao servidor. Normalmente, é criado um thread de sistema operacional separado para cada solicitação de consulta. Porém, com centenas de conexões para o servidor, usam um thread por solicitação de consulta pode consumir quantias grandes de recursos do sistema. A opção **max worker threads** habilita o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criar um pool de threads de trabalho para atender a um número maior de solicitações de consulta, o que melhora o desempenho.  
  
-   A tabela a seguir mostra o número configurado automaticamente de máximo de threads de trabalho para várias combinações de CPUs e versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    |Número de CPUs|Computador de 32 bits|Computador de 64 bits|  
    |--------------------|----------------------|----------------------|  
    |\<= 4 processadores|256|512|  
    |8 processadores|288|576|  
    |16 processadores|352|704|  
    |32 processadores|480|960|  
    |64 processadores|736|1.472|  
    |128 processadores|4.224|4.480|  
    |256 processadores|8.320|8.576|  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode mais ser instalado em um sistema operacional de 32 bits. Valores de computador de 32 bits são listados para a assistência aos clientes que executam o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versões anteriores.   É recomendável 1024 como o número máximo de threads de trabalho para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado em um computador de 32 bits.  
  
    > [!NOTE]  
    >  Para obter recomendações sobre como usar mais de 64 CPUs, veja [Práticas recomendadas para executar o SQL Server em computadores que têm mais de 64 CPUs](http://technet.microsoft.com/library/ee210547\(SQL.105\).aspx).  
  
-   Quando todos os threads de trabalho estiverem ativos com a execução de consultas longas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá parecer não estar respondendo até que um thread de trabalho seja concluído e fique disponível. Embora não seja um defeito, isso às vezes pode ser indesejável. Se um processo parecer ser não estar respondendo e nenhuma nova consulta possa ser processada, então conecte ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa a conexão de administrador dedicada (DAC) e elimine o processo. Para evitar isto, aumente o número de máximo threads de trabalho.  
  
 A opção de configuração do servidor**max worker threads** não leva em consideração os threads necessários para todas as tarefas de sistema como grupos de disponibilidade, Service Broker, Gerenciador de Bloqueio dentre outros.  Se o número de threads configurados estiver sendo excedido, a seguinte consulta fornecerá informações sobre as tarefas do sistema que geraram os threads adicionais.  
  
```  
SELECT  
s.session_id,  
r.command,  
r.status,  
r.wait_type,  
r.scheduler_id,  
w.worker_address,  
w.is_preemptive,  
w.state,  
t.task_state,  
t.session_id,  
t.exec_context_id,  
t.request_id  
FROM sys.dm_exec_sessions AS s  
INNER JOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
WHERE s.is_user_process = 0;  
  
```  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Para configurar a opção max worker threads  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Processadores** .  
  
3.  Na caixa **Máximo de threads de trabalho** , digite ou selecione um valor entre 128 e 32767.  
  
     Use a opção **max worker threads** para configurar o número de threads de trabalho disponível para os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A configuração padrão para **max worker threads** é a melhor para a maioria dos sistemas. No entanto, dependendo de sua configuração de sistema, definir **máximo de threads de trabalho** como um valor menor algumas vezes melhora o desempenho.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Para configurar a opção max worker threads  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar o [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar a opção `max worker threads` como `900`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obter mais informações, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção max worker threads  
 A alteração entrará em vigor imediatamente sem exigir que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reinicie.  
  
## <a name="see-also"></a>Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  

