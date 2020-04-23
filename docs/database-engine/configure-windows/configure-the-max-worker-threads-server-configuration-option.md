---
title: Configurar a opção de configuração de servidor max worker threads | Microsoft Docs
ms.custom: ''
ms.date: 04/14/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d573bc4c8fc628bf4f1cc1fa36e50bc0e69c3202
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488309"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>Configurar a opção max worker threads de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **max worker threads** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **max worker threads** configura o número de threads de trabalho que estão disponíveis para os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os serviços de thread nativos dos sistemas operacionais de forma que um ou mais threads ofereçam suporte a cada rede à qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte simultaneamente, outro thread controle pontos de verificação de banco de dados e um pool de threads controle todos os usuários. O valor padrão de **max worker threads** é 0. Isso habilita o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a configurar automaticamente o número de threads de trabalho na inicialização. A configuração padrão é a melhor para a maioria dos sistemas. No entanto, dependendo de sua configuração de sistema, a definição de **max worker threads** com um valor específico às vezes melhora o desempenho.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção max worker threads, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [após você configurar a opção max worker threads](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Quando o número real de solicitações de consulta é menor que a quantidade definida em **max worker threads**, um thread controla cada solicitação de consulta. Porém, se o número real de solicitação de consulta exceder a quantia definida em **max worker threads**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará o pool dos threads de trabalho de forma que próximo thread de trabalho disponível possa controlar a solicitação.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado. Se você suspeitar que há um problema de desempenho, é provável que não seja a disponibilidade dos threads de trabalho. A causa mais provável é que algo, como a E/S, está fazendo com que os threads de trabalho aguardem. É melhor localizar a causa raiz de um problema de desempenho antes de alterar a configuração max worker threads.  
  
-   O thread pooling ajuda a otimizar o desempenho quando são conectados grandes números de clientes ao servidor. Normalmente, é criado um thread de sistema operacional separado para cada solicitação de consulta. Porém, com centenas de conexões para o servidor, usam um thread por solicitação de consulta pode consumir quantias grandes de recursos do sistema. A opção **max worker threads** habilita o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criar um pool de threads de trabalho para atender a um número maior de solicitações de consulta, o que melhora o desempenho.  
  
-   A tabela a seguir mostra o número máximo automaticamente configurado de threads de trabalho para várias combinações de CPUs, arquitetura de computador e versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando a fórmula: * **Máximo de trabalhos padrão* + ((* CPUs lógicas *-4) * *trabalhos por CPU*) * *.  
  
    |Número de CPUs|Computador de 32 bits (até [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])|Computador de 64 bits (até [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1)|Computador de 64 bits (começando em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])|   
    |------------|------------|------------|------------|  
    |\< = 4|256|512|512|   
    |8|288|576|576|   
    |16|352|704|704|   
    |32|480|960|960|   
    |64|736|1\.472|2432|   
    |128|1248|2496|4480|   
    |256|2272|4544|8\.576|   
    
    Até [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, os *Trabalhos por CPU* só dependem da arquitetura (32 bits ou 64 bits):
    
    |Número de CPUs|Computador de 32 bits <sup>1</sup>|Computador de 64 bits|   
    |------------|------------|------------|   
    |\< = 4|256|512|   
    |\> 4|256 + (do (CPU lógica - 4) * 8)|512 <sup>2</sup> + ((CPUs lógicas – 4) * 16)|   
    
    A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], os *Trabalhos por CPU* dependem da arquitetura e do número de processadores (entre 4 e 64 ou maior que 64):
    
    |Número de CPUs|Computador de 32 bits <sup>1</sup>|Computador de 64 bits|   
    |------------|------------|------------|   
    |\< = 4|256|512|   
    |\> 4 e \<= 64|256 + (do (CPU lógica - 4) * 8)|512 <sup>2</sup> + ((CPUs lógicas – 4) * 16)|   
    |\> 64|256 + ((CPUs lógicas – 4) * 32)|512 <sup>2</sup> + ((CPUs lógicas – 4) * 32)|   
  
    <sup>1</sup> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode mais ser instalado em um sistema operacional de 32 bits. Valores de computador de 32 bits são listados para a assistência aos clientes que executam o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versões anteriores. É recomendável 1.024 como o número máximo de threads de trabalho para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado em um computador de 32 bits.
    
    <sup>2</sup> A partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], o valor *Máximo de trabalhos padrão* é dividido por 2 para computadores com menos de 2 GB de memória.
  
    > [!TIP]  
    > Para obter recomendações sobre como usar mais de 64 CPUs, veja [Práticas recomendadas para executar o SQL Server em computadores que têm mais de 64 CPUs](../../relational-databases/thread-and-task-architecture-guide.md#best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus).  
  
-   Quando todos os threads de trabalho estiverem ativos com a execução de consultas longas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá parecer não estar respondendo até que um thread de trabalho seja concluído e fique disponível. Embora não seja um defeito, isso às vezes pode ser indesejável. Se um processo parecer ser não estar respondendo e nenhuma nova consulta possa ser processada, então conecte ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa a conexão de administrador dedicada (DAC) e elimine o processo. Para evitar isto, aumente o número de máximo threads de trabalho.  
  
 A opção **max worker threads** da configuração do servidor não limita todos os threads que podem ser gerados no sistema. Os threads necessários para tarefas, como Grupos de Disponibilidade, Service Broker, Gerenciador de Bloqueio ou outros, são gerados fora desse limite. Se o número de threads configurados for excedido, a consulta a seguir fornecerá informações sobre as tarefas do sistema que geraram os threads adicionais.  
  
 ```sql  
 SELECT  s.session_id, r.command, r.status,  
    r.wait_type, r.scheduler_id, w.worker_address,  
    w.is_preemptive, w.state, t.task_state,  
    t.session_id, t.exec_context_id, t.request_id  
 FROM sys.dm_exec_sessions AS s  
 INNER JOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
 INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
 INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
 WHERE s.is_user_process = 0;  
 ```  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução `RECONFIGURE`, o usuário deve ter a permissão `ALTER SETTINGS` no nível do servidor. A permissão `ALTER SETTINGS` é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin**.  
  
##  <a name="using-ssmanstudiofull"></a><a name="SSMSProcedure"></a> Usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Para configurar a opção max worker threads  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Processadores** .  
  
3.  Na caixa **max worker threads**, digite ou selecione um valor entre 128 e 32.767.  
  
> [!TIP]
> Use a opção **max worker threads** para configurar o número de threads de trabalho disponível para os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A configuração padrão para **max worker threads** é a melhor para a maioria dos sistemas. No entanto, dependendo de sua configuração de sistema, definir **máximo de threads de trabalho** como um valor menor algumas vezes melhora o desempenho.
> Consulte as [Recomendações](#Recommendations) nesta página para obter mais informações.
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>Para configurar a opção max worker threads  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar o [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar a opção `max worker threads` como `900`.  
  
```sql  
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
  
##  <a name="follow-up-after-you-configure-the-max-worker-threads-option"></a><a name="FollowUp"></a> Acompanhamento: Após você configurar a opção max worker threads  
 A alteração entrará em vigor imediatamente após a execução da opção [RECONFIGURAR](../../t-sql/language-elements/reconfigure-transact-sql.md), sem exigir que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] seja reiniciado.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
