---
title: Pontos de verificação de banco de dados (SQL Server) | Microsoft Docs
ms.date: 09/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
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
caps.latest.revision: 74
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dd0160149410a5de96158f1137972fcafdbeba8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="database-checkpoints-sql-server"></a>Pontos de verificação de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 Um *ponto de verificação* cria um bom ponto conhecido a partir do qual o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] pode começar a aplicar as alterações contidas no log durante a recuperação após um desligamento ou uma falha inesperada.  
 
  
##  <a name="Overview"></a> Visão geral   
Por razões de desempenho, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] executa modificações nas páginas de banco de dados — no cache do buffer — e não grava essas páginas em disco após cada alteração. Em vez disso, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emite um ponto de verificação periodicamente em cada banco de dados. Um *ponto de verificação* grava as páginas atuais modificadas na memória (conhecidas como *páginas sujas*) e as informações do log de transações de memória para disco e, além disso, registra informações sobre o log de transações.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferece suporte para vários tipos de pontos de verificação: automáticos, indiretos, manuais e internos. A seguinte tabela resume os tipos de **pontos de verificação:**
  
|Nome|[!INCLUDE[tsql](../../includes/tsql-md.md)] Interface|Description|  
|----------|----------------------------------|-----------------|  
|Automatic|EXEC sp_configure **'** recovery interval **','***seconds***'**|Emitido automaticamente em segundo plano para seguir de tempo superior sugerido pela opção de configuração de servidor **recovery interval** . Pontos de verificação automáticos executados até a conclusão.  Os pontos de verificação automáticos são limitados com base no número de gravações pendentes e se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] detectar um aumento na latência de gravação acima de 50 milissegundos.<br /><br /> Para obter mais informações, consulte [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).|  
|Indireto.|ALTER DATABASE … SET TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS &#124; MINUTES }|Emitido em segundo plano para cumprir um horário de recuperação de destino especificado pelo usuário para um determinado banco de dados. A partir do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)], o valor padrão é de 1 minuto. O padrão é 0 para versões mais antigas, o que indica que o banco de dados usará pontos de verificação automáticos cuja frequência depende da configuração do intervalo de recuperação da instância de servidor.<br /><br /> Para obter mais informações, consulte [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md).|  
|Manual|CHECKPOINT [ *checkpoint_duration* ]|Emitido quando você executa um comando [!INCLUDE[tsql](../../includes/tsql-md.md)] CHECKPOINT. O ponto de verificação manual ocorre no banco de dados atual para sua conexão. Por padrão, pontos de verificação manuais são executados até a conclusão. A aceleração funciona da mesma forma que para pontos de verificação automáticos.  Opcionalmente, o parâmetro *checkpoint_duration* especifica a quantidade de tempo solicitada, em segundos, para a conclusão do ponto de verificação.<br /><br /> Para obter mais informações, consulte [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md).|  
|Internal|Nenhum.|Emitido por várias operações de servidor, como backup e criação de instantâneo de banco de dados, para garantir que as imagens de disco coincidam com o estado atual do log.|  
  
> [!NOTE]
> A opção de configuração avançada **-k** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que um administrador de banco de dados acelere o comportamento de E/S do ponto de verificação com base na taxa de transferência do subsistema de E/S de alguns tipos de pontos de verificação. A opção de configuração **-k** se aplica a pontos de verificação automáticos e a qualquer ponto de verificação manual e interno.  
  
 Para pontos de verificação automáticos, manuais e internos, somente as modificações feitas após o último ponto de verificação devem passar por roll forward durante a recuperação de banco de dados. Isso reduz o tempo necessário para recuperar um banco de dados.  
  
> [!IMPORTANT]
> Transações não confirmadas de execução longa aumentam o tempo de recuperação para todos os tipos de pontos de verificação.   
  
##  <a name="InteractionBwnSettings"></a> Interação de TARGET_RECOVERY_TIME e opções 'recovery interval'  
 A tabela a seguir resume a interação entre a configuração do servidor **sp_configure'** recovery interval **'** de todo o servidor e a configuração ALTER DATABASE... específica do banco de dados. TARGET_RECOVERY_TIME.  
  
|target_recovery_time|'recovery interval'|Tipo de ponto de verificação usado|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|pontos de verificação automáticos cujo intervalo de recuperação de destino é 1 minuto.|  
|0|>0|Pontos de verificação automáticos, cujo intervalo de recuperação de destino é especificado pela configuração definida pelo usuário na opção **sp_configurerecovery interval**.|  
|>0|Não aplicável.|Pontos de verificação indiretos cuja hora de recuperação de destino é determinada pela configuração de TARGET_RECOVERY_TIME, expressa em segundos.|  
  
##  <a name="AutomaticChkpt"></a> Pontos de verificação automáticos  
Um ponto de verificação automático ocorre sempre que o número de registros de log atinge o número que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima que pode processar durante o tempo especificado na opção de configuração do servidor **recovery interval** . 
 
Em todo banco de dados sem uma hora de recuperação de destino definida pelo usuário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] gera pontos de verificação automáticos. A frequência depende da opção de configuração de servidor avançada **recovery interval** , que especifica o tempo máximo que determinada instância de servidor deve usar para recuperar um banco de dados durante uma reinicialização do sistema. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] estima o número máximo de registros de log que pode processar no intervalo de recuperação. Quando um banco de dados que usa alcances de pontos de verificação automáticos atinge o número máximo de registros de log, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emite um ponto de verificação no banco de dados. 
 
O intervalo de tempo entre pontos de verificação automáticos pode ser **altamente** variável. Um banco de dados com uma carga de trabalho de transações significativa terá mais pontos de verificação frequentes do que um banco de dados usado principalmente para operações somente leitura. No modelo de recuperação simples, um ponto de verificação automático também será colocado na fila se o log se tornar 70% cheio.  
  
No modelo de recuperação simples, a menos que algum fator esteja atrasando o truncamento do log, um ponto de verificação automático trunca a seção não usada do log de transações. Em contrapartida, nos modelos de recuperação completo e bulk-logged, após o estabelecimento de uma cadeia de backup de log, os pontos de verificação automáticos não causam truncamento de log. Para obter mais informações, consulte [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
Depois de uma falha do sistema, o tempo necessário para recuperar determinado banco de dados depende em grande parte da quantidade de E/S aleatória necessária para refazer páginas que estavam sujas no momento da falha. Isso significa que a configuração de **recovery interval** não é confiável. Não é possível determinar uma duração de recuperação precisa. Além disso, quando um ponto de verificação automático está em andamento, a atividade de E/S geral para os dados aumenta significativamente e de forma bastante imprevisível.  
   
###  <a name="PerformanceImpact"></a> Impacto do intervalo de recuperação no desempenho de recuperação  
Para um sistema de processamento de transações online usando transações curtas (OLTP), o **recovery interval** é o fator primário que determina o tempo da recuperação. No entanto, a opção **recovery interval** não afeta o tempo necessário para desfazer uma transação de longa duração. A recuperação de um banco de dados com uma transação de longa duração pode levar mais tempo do que o especificado na opção **recovery interval** . 
 
Por exemplo, se uma transação demorada levou duas horas para executar atualizações antes que a instância do servidor fosse desabilitada, a recuperação real levará um tempo consideravelmente mais longo do que o valor de **recovery interval** para recuperar a transação demorada. Para obter mais informações sobre o impacto de uma transação de longa duração em um tempo de recuperação, veja [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
Normalmente, os valores padrão fornecem um ótimo desempenho de recuperação. No entanto, a alteração do intervalo de recuperação pode melhorar o desempenho nas circunstâncias seguintes:  
  
-   Se, em geral, a recuperação demorar significativamente mais que 1 minuto quando transações demoradas não estão sendo revertidas.  
  
-   Se você notar que os pontos de verificação frequentes estão prejudicando o desempenho em um banco de dados.  
  
Se você decidir aumentar a configuração **recovery interval** , recomendamos fazer isso gradativamente em pequenos incrementos e avaliar o efeito de cada aumento incremental no desempenho de recuperação. Esse método é importante porque, à medida que a configuração **recovery interval** aumenta, a recuperação de banco de dados demora mais tempo para ser concluída. Por exemplo, se você alterar **recovery interval** para 10 minutos, a recuperação levará aproximadamente 10 vezes mais tempo para ser concluída do que se **recovery interval** tivesse sido definido para um minuto.  
  
##  <a name="IndirectChkpt"></a> Pontos de verificação indiretos  
Pontos de verificação indiretos, introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], fornecem uma alternativa de nível de banco de dados configurável para os pontos de verificação automáticos. No caso de uma falha de sistema, pontos de verificação indiretos fornecem um tempo de recuperação mais previsível potencialmente mais rápido do que os pontos de verificação automáticos. Os pontos de verificação indiretos oferecem as seguintes vantagens:  
  
-   Uma carga de trabalho transacional online em um banco de dados configurado para pontos de verificação indiretos pode apresentar degradação no desempenho. Pontos de verificação indiretos garantem que o número de páginas sujas fica abaixo de determinado limite, para que a recuperação do banco de dados seja concluída dentro da meta do tempo de recuperação. 

A opção de configuração do intervalo de recuperação usa o número de transações para determinar o tempo de recuperação em relação aos pontos de verificação indiretos, que usam o número de páginas sujas. Quando pontos de verificação indiretos são habilitados em um banco de dados que recebe um grande número de operações DML, o gravador em segundo plano pode iniciar eliminação agressiva de buffers sujos no disco para garantir que o tempo necessário para executar a recuperação esteja dentro da meta do tempo de recuperação definido para o banco de dados. Isso pode causar atividade adicional de E/S em determinados sistemas, o que pode contribuir para um gargalo de desempenho, se o subsistema do disco estiver operando acima ou próximo do limite de E/S.  
  
-   Pontos de verificação indiretos permitem a você controlar o tempo de recuperação de banco de dados de modo confiável, fatorando no custo de E/S aleatória durante REDO. Isso permite que uma instância de servidor permaneça em um limite superior nos tempos de recuperação para um determinado banco de dados (exceto quando uma transação demorada causa tempos UNDO excessivos).  
  
-   Pontos de verificação indiretos reduzem os picos de E/S relacionados ao ponto de verificação gravando continuamente páginas sujas em disco em segundo plano.  
  
No entanto, uma carga de trabalho transacional online em um banco de dados configurado para pontos de verificação indiretos pode apresentar degradação no desempenho. Isso ocorre porque o gravador em segundo plano usado pelo ponto de verificação indireto às vezes aumenta a carga de gravação total de uma instância de servidor.  
 
> [!IMPORTANT]
> O ponto de verificação indireto é o comportamento padrão de novos bancos de dados criados no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], incluindo os bancos de dados de Modelo de TempDB.          
> Os bancos de dados atualizados no local ou restaurados com base em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usarão o comportamento de ponto de verificação automático anterior, a menos que tenham sido explicitamente alterados para usar o ponto de verificação indireto.       
  
##  <a name="EventsCausingChkpt"></a> Pontos de verificação internos  
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
  
-   [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **Para emitir um ponto de verificação manual em um banco de dados**  
  
-   [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  

  
## <a name="see-also"></a>Confira também  
[O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)            
[Arquitetura física do log de transações](http://technet.microsoft.com/library/ms179355.aspx) (dos [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Manuais Online, mas ainda aplicável)       
  
  
