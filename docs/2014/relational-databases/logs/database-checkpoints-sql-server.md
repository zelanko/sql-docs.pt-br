---
title: Pontos de verificação de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- automatic checkpoints
- transaction logs [SQL Server], checkpoints
- logs [SQL Server], active
- pages [SQL Server], dirty
- MinLSN
- checkpoints [SQL Server]
- pages [SQL Server], flushing
- dirty pages
- transaction logs [SQL Server], active logs
- recovery interval option [SQL Server]
- buffer cache [SQL Server]
- logs [SQL Server], checkpoints
- Minimum Recovery LSN
- flushing pages
- active logs
ms.assetid: 98a80238-7409-4708-8a7d-5defd9957185
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b0271c21b849ee754e0050ea461c86d1f773850
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058526"
---
# <a name="database-checkpoints-sql-server"></a>Pontos de verificação de banco de dados (SQL Server)
  Este tópico fornece uma visão geral dos pontos de verificação de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um *ponto de verificação* cria um bom ponto conhecido a partir do qual o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] pode começar a aplicar as alterações contidas no log durante a recuperação após um desligamento ou uma falha inesperada.  
  
  
##  <a name="Overview"></a> Visão geral dos pontos de verificação  
 Por razões de desempenho, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] executa modificações nas páginas de banco de dados — no cache do buffer — e não grava essas páginas em disco após cada alteração. Em vez disso, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emite um ponto de verificação periodicamente em cada banco de dados. Um *ponto de verificação* grava as páginas atuais modificadas na memória (conhecidas como *páginas sujas*) e as informações do log de transações de memória para disco e, além disso, registra informações sobre o log de transações.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferece suporte para vários tipos de pontos de verificação: automáticos, indiretos, manuais e internos. A tabela a seguir resume os tipos de pontos de verificação.  
  
|Nome|[!INCLUDE[tsql](../../includes/tsql-md.md)] Interface|Description|  
|----------|----------------------------------|-----------------|  
|Automatic|EXEC sp_configure **'`recovery interval`','*`seconds`*'**|Emitido automaticamente em segundo plano para atender o limite de tempo superior sugerido pelo `recovery interval` opção de configuração do servidor. Pontos de verificação automáticos executados até a conclusão.  Os pontos de verificação automáticos são acelerados com base no número de gravações pendentes e se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] detecta um aumento na latência de gravação acima de 20 milissegundos.<br /><br /> Para obter mais informações, consulte [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).|  
|Indireto.|ALTER DATABASE … SET TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS &#124; MINUTES }|Emitido em segundo plano para cumprir um horário de recuperação de destino especificado pelo usuário para um determinado banco de dados. A hora de recuperação de destino padrão é 0, o que faz com que a heurística de ponto de verificação automático seja usada no banco de dados. Se você usou ALTER DATABASE para definir TARGET_RECOVERY_TIME a >0, esse valor será usado, em vez do intervalo de recuperação especificado para a instância do servidor.<br /><br /> Para obter mais informações, veja [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](change-the-target-recovery-time-of-a-database-sql-server.md).|  
|Manual|CHECKPOINT [ *checkpoint_duration* ]|Emitido quando você executa um comando [!INCLUDE[tsql](../../includes/tsql-md.md)] CHECKPOINT. O ponto de verificação manual ocorre no banco de dados atual para sua conexão. Por padrão, pontos de verificação manuais são executados até a conclusão. A aceleração funciona da mesma forma que para pontos de verificação automáticos.  Opcionalmente, o parâmetro *checkpoint_duration* especifica a quantidade de tempo solicitada, em segundos, para a conclusão do ponto de verificação.<br /><br /> Para obter mais informações, consulte [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql).|  
|Internal|Nenhum.|Emitido por várias operações de servidor, como backup e criação de instantâneo de banco de dados, para garantir que as imagens de disco coincidam com o estado atual do log.|  
  
> [!NOTE]  
>  O `-k` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opção de configuração avançada permite que um administrador de banco de dados para o comportamento de e/s com base na taxa de transferência do subsistema de e/s para alguns tipos de pontos de verificação do ponto de verificação de restrição. O `-k` opção de configuração se aplica a pontos de verificação automáticos e a qualquer ponto de verificação manual e interna.  
  
 Para pontos de verificação automáticos, manuais e internos, somente as modificações feitas após o último ponto de verificação devem passar por roll forward durante a recuperação de banco de dados. Isso reduz o tempo necessário para recuperar um banco de dados.  
  
> [!IMPORTANT]  
>  Transações não confirmadas de execução longa aumentam o tempo de recuperação para todos os tipos de pontos de verificação.  
  
  
  
###  <a name="InteractionBwnSettings"></a> Interação de TARGET_RECOVERY_TIME e opções 'recovery interval'  
 A tabela a seguir resume a interação entre o todo o servidor **sp_configure'`recovery interval`'** configuração e específicas do banco de dados ALTER DATABASE... TARGET_RECOVERY_TIME.  
  
|target_recovery_time|'recovery interval'|Tipo de ponto de verificação usado|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|pontos de verificação automáticos cujo intervalo de recuperação de destino é 1 minuto.|  
|0|>0|Pontos de verificação automáticos, cujo intervalo de recuperação de destino é especificado pela configuração definida pelo usuário na opção **sp_configurerecovery interval**.|  
|>0|Não aplicável.|Pontos de verificação indiretos cuja hora de recuperação de destino é determinada pela configuração de TARGET_RECOVERY_TIME, expressa em segundos.|  
  
###  <a name="AutomaticChkpt"></a> Pontos de verificação automáticos  
 Um ponto de verificação automático ocorre cada vez que o número de registros de log atinge o número de [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima que pode processar durante o tempo especificado no `recovery interval` opção de configuração do servidor. Em todo banco de dados sem uma hora de recuperação de destino definida pelo usuário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera pontos de verificação automáticos. A frequência de pontos de verificação automáticos depende o `recovery interval` avançados a opção de configuração de servidor, que especifica o tempo máximo que uma determinada instância de servidor deve usar para recuperar um banco de dados durante uma reinicialização do sistema. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima o número máximo de registros de log que pode processar no intervalo de recuperação. Quando um banco de dados que está usando alcances de pontos de verificação automáticos atinge o número máximo de registros de log, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emite um ponto de verificação no banco de dados. O intervalo de tempo entre pontos de verificação automáticos pode ser altamente variável. Um banco de dados com uma carga de trabalho de transações significativa terá mais pontos de verificação frequentes que um banco de dados usado principalmente para operações somente leitura.  
  
 Além disso, no modelo de recuperação simples, um ponto de verificação automático também será enfileirado se o log se tornar 70% cheio.  
  
 No modelo de recuperação simples, a menos que algum fator esteja atrasando o truncamento do log, um ponto de verificação automático trunca a seção não usada do log de transações. Em contrapartida, nos modelos de recuperação completo e bulk-logged, após o estabelecimento de uma cadeia de backup de log, os pontos de verificação automáticos não causam truncamento de log. Para obter mais informações, veja [O log de transações &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
 Depois de uma falha do sistema, o tempo necessário para recuperar um determinado banco de dados depende muito da quantidade de E/S aleatória necessária para refazer páginas que estavam sujas no momento da falha. Isso significa que o `recovery interval` configuração não é confiável. Não é possível determinar uma duração de recuperação precisa. Além disso, quando um ponto de verificação automático está em andamento, a atividade de E/S geral para os dados aumenta significativamente e de forma bastante imprevisível.  
  
  
####  <a name="PerformanceImpact"></a> Impacto do intervalo de recuperação no desempenho de recuperação  
 Para um sistema (OLTP) usando transações curtas, de processamento de transações online `recovery interval` é o principal fator que determina o tempo de recuperação. No entanto, o `recovery interval` opção não afeta o tempo necessário para desfazer uma transação de longa execução. Recuperação de um banco de dados com uma transação de longa execução pode levar muito mais do que o especificado no `recovery interval` opção. Por exemplo, se uma transação demorada levou duas horas para executar atualizações antes que a instância do servidor fosse desabilitada, a recuperação real levará consideravelmente mais longo que o `recovery interval` valor para recuperar a transação demorada. Para obter mais informações sobre o impacto de uma transação de longa duração em um tempo de recuperação, veja [O log de transações &#40;SQL Server&#41;](the-transaction-log-sql-server.md).  
  
 Normalmente, os valores padrão fornecem um ótimo desempenho de recuperação. No entanto, a alteração do intervalo de recuperação pode melhorar o desempenho nas circunstâncias seguintes:  
  
-   Se, em geral, a recuperação demorar significativamente mais que 1 minuto quando transações demoradas não estão sendo revertidas.  
  
-   Se você notar que os pontos de verificação frequentes estão prejudicando o desempenho em um banco de dados.  
  
 Se você decidir aumentar a configuração `recovery interval`, recomendamos fazer isso gradativamente em pequenos incrementos e avaliar o efeito de cada aumento incremental no desempenho de recuperação. Essa abordagem é importante porque como o `recovery interval` definindo aumenta, recuperação de banco de dados demora muitas vezes para concluir. Por exemplo, se você alterar `recovery interval` 10, a recuperação levará aproximadamente 10 vezes mais demorado que se `recovery interval` é definido como zero.  
  
  
###  <a name="IndirectChkpt"></a> Pontos de verificação indiretos  
 Pontos de verificação indiretos, novos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], fornecem um nível de banco de dados configurável alternativo para pontos de verificação automáticos. No caso de uma falha de sistema, pontos de verificação indiretos fornecem um tempo de recuperação mais previsível potencialmente mais rápido do que os pontos de verificação automáticos. Os pontos de verificação indiretos oferecem as seguintes vantagens:  
  
-   Uma carga de trabalho transacional online em um banco de dados configurado para pontos de verificação indiretos pode apresentar degradação no desempenho. Pontos de verificação indiretos garantem que o número de páginas sujas esteja abaixo de certo limite, para que a recuperação do banco de dados seja concluída dentro da meta do tempo de recuperação. A opção de configuração do intervalo de recuperação usa o número de transações para determinar o tempo de recuperação em relação aos pontos de verificação indiretos, que usam o número de páginas sujas. Quando pontos de verificação indiretos são habilitados em um banco de dados que recebe um grande número de operações DML, o gravador em segundo plano pode iniciar eliminação agressiva de buffers sujos no disco para garantir que o tempo necessário para executar a recuperação esteja dentro da meta do tempo de recuperação definido para o banco de dados. Isso pode causar atividade adicional de E/S em determinados sistemas, o que pode contribuir para um gargalo de desempenho, se o subsistema do disco estiver operando acima ou próximo do limite de E/S.  
  
-   Pontos de verificação indiretos permitem a você controlar o tempo de recuperação de banco de dados de modo confiável, fatorando no custo de E/S aleatória durante REDO. Isso permite que uma instância de servidor permaneça em um limite superior nos tempos de recuperação para um determinado banco de dados (exceto quando uma transação demorada causa tempos UNDO excessivos).  
  
-   Pontos de verificação indiretos reduzem os picos de E/S relacionados ao ponto de verificação gravando continuamente páginas sujas em disco em segundo plano.  
  
 No entanto, uma carga de trabalho transacional online em um banco de dados configurado para pontos de verificação indiretos podem apresentar degradação no desempenho. Isso ocorre porque o gravador em segundo plano usado pelo ponto de verificação indireto às vezes aumenta a carga de gravação total de uma instância de servidor.  
  
  
###  <a name="EventsCausingChkpt"></a> Pontos de verificação internos  
 Os pontos de verificação internos são gerados por vários componentes de servidor para garantir que as imagens de disco correspondam ao estado atual do log. Pontos de verificação internos são gerados em resposta aos eventos seguintes:  
  
-   Os arquivos de banco de dados foram adicionados ou removidos usando ALTER DATABASE.  
  
-   É realizado um backup de banco de dados.  
  
-   Um instantâneo de banco de dados é criado, explicitamente ou internamente para DBCC CHECK.  
  
-   É executada uma atividade que requer um desligamento de banco de dados. Por exemplo, AUTO_CLOSE está ON e a última conexão de usuário com o banco de dados está fechada ou é feita uma modificação de opção de banco de dados que requer o reinício do banco de dados.  
  
-   Uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é interrompida com a interrupção do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER). Qualquer ação causa um ponto de verificação em cada banco de dados na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Colocando uma FCI (instância de cluster de failover) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline.  
  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para alterar o intervalo de recuperação em uma instância de servidor**  
  
-   [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)  
  
 **Para configurar pontos de verificação indiretos em um banco de dados**  
  
-   [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **Para emitir um ponto de verificação manual em um banco de dados**  
  
-   [CHECKPOINT &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/checkpoint-transact-sql)  
  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Arquitetura física do log de transações](http://technet.microsoft.com/library/ms179355.aspx) (nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)])  
  
  
## <a name="see-also"></a>Consulte também  
 [O log de transações &#40;SQL Server&#41;](the-transaction-log-sql-server.md)  
  
  
