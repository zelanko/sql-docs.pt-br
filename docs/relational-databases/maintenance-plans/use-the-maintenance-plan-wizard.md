---
title: Usar o Assistente de Plano de Manutenção | Microsoft Docs
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.ag.maintwiz.integrity.f1
- sql13.ag.maintwiz.order.f1
- sql13.ag.maintwiz.report.f1
- sql13.ag.maintwiz.updatestats.f1
- sql13.ag.maintwiz.indexdefrag.f1
- sql13.ag.maintwiz.progress.f1
- sql13.ag.maintwiz.maintcleanup.f1
- sql13.ag.maintwiz.backupfull.f1
- sql13.ag.maintwiz.task.f1
- sql13.ag.maintwiz.server.f1
- sql13.ag.maintwiz.shrinkdb.f1
- sql13.ag.maintwiz.execagentjob.f1
- sql13.ag.maintwiz.summary.f1
- sql13.ag.maintwiz.welcome.f1
- sql13.ag.maintwiz.planprop.f1
- sql13.ag.maintwiz.reindex.f1
- sql13.ag.maintwiz.histcleanup.f1
- sql13.ag.maintwiz.backuplog.f1
- sql13.ag.maintwiz.backupdiff.f1
helpviewer_keywords:
- Maintenance Plan Wizard
- Database Maintenance Plan Wizard
- Database Maintenance Plan Wizard, starting
ms.assetid: db65c726-9892-480c-873b-3af29afcee44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 533447273bb174eadeace6cd3b8a2b2f95504811
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544151"
---
# <a name="use-the-maintenance-plan-wizard"></a>Usar o Assistente de Plano de Manutenção
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar um plano de manutenção de um único servidor ou de vários servidores usando o Assistente de Plano de Manutenção no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O Assistente de Plano de Manutenção cria um plano de manutenção que pode ser executado regularmente pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Isso permite executar várias tarefas de administração de banco de dados, incluindo backups, verificações de integridade de banco de dados ou atualizações de estatísticas de banco de dados em intervalos especificados.  
    
 
##  <a name="Restrictions"></a> Limitações e restrições  
  
-   Para criar um plano de manutenção multisservidor, é necessário configurar um ambiente multisservidor com um servidor mestre e um ou mais servidores de destino. Você deve criar e manter planos de manutenção multisservidor no servidor mestre. Você pode exibir planos nos servidores de destino.   

-   Os membros das funções **db_ssisadmin** e **dc_admin** podem elevar seus privilégios para **sysadmin**. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ; esses pacotes podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança **sysadmin** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. 

Para se proteger contra essa elevação de privilégio ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros **sysadmin** às funções **db_ssisadmin** e **dc_admin** .  

##  <a name="Prerequisite"></a> Pré-requisitos 
Você deve habilitar a [Opção Agent XPs de configuração do servidor](../../database-engine/configure-windows/agent-xps-server-configuration-option.md).
  
  
##  <a name="Permissions"></a> Permissões  
 Para criar ou gerenciar planos de manutenção, é necessário ser membro da função de servidor fixa **sysadmin** . O Pesquisador de Objetos só exibe o nó **Planos de Manutenção** para usuários que são membros da função de servidor fixa **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usar o Assistente de Plano de Manutenção  
  
**Inicie o assistente** 

  
1.  Expanda o servidor no qual você deseja criar seu plano de gerenciamento.  
  
2.  Expanda a pasta **Gerenciamento** .  
  
3.  Clique com o botão direito do mouse na pasta **Planos de Manutenção** e selecione **Assistente de Plano de Manutenção**.  
  
4.  Na página **Assistente de Plano de Manutenção do SQL Server** , clique em **Avançar**.  
  
5.  Na página **Selecionar Propriedades do Plano** :  
  
    1.  Na caixa **Nome** , insira o nome do plano de manutenção que você está criando.  
  
    2.  Na caixa **Descrição** , descreva brevemente seu plano de manutenção.  
  
    3.  Na lista **Executar como** , especifique a credencial usada pelo Microsoft SQL Server Agent ao executar o plano de manutenção.  
  
    4.  Selecione **Agendas separadas para cada tarefa** ou **Agenda única para o plano inteiro ou sem agenda** para especificar a agenda recorrente do plano de manutenção.  
  
        > **OBSERVAÇÃO:** se você selecionar **Agendamentos separados para cada tarefa**, será necessário executar as etapas de **e.** a seguir para cada tarefa do plano de manutenção.  
  
    5.  Se você selecionou **Agenda única para o plano inteiro ou sem agenda**, em **Agenda**, clique em **Alterar**.  
  
        1.  Na caixa de diálogo **Nova Agenda de Trabalho**, na caixa **Nome**, digite o nome da agenda de trabalho.  
  
        2.  Na lista **Tipo de Agenda** , selecione o tipo de agenda:  
  
            -   **Iniciar automaticamente quando o SQL Server Agent for iniciado**  
  
            -   **Iniciar sempre que as CPUs estiverem ociosas**  
  
            -   **Recorrente**. Essa é a seleção padrão.  
  
            -   **Uma vez**  
  
        3.  Marque ou desmarque a caixa de seleção **Habilitado** para habilitar ou desabilitar a agenda.  
  
        4.  Se você selecionar **Recorrente**:  
  
            1.  Em **Frequência**, na lista **Ocorre** , especifique a frequência de ocorrência:  
  
                -   Se você selecionar **Diário**, na caixa **Ocorre periodicamente a cada** , digite a frequência com que a agenda de trabalho se repete em dias.  
  
                -   Se você selecionar **Semanal**, na caixa **Ocorre periodicamente a cada** , digite a frequência com que a agenda de trabalho se repete em semanas. Selecione o dia da semana em que a agenda de trabalho é executada.  
  
                -   Se você selecionar **Mensalmente**, selecione **Dia** ou **O**.  
  
                    -   Se você selecionar **Dia**, digite o dia do mês que você deseja que a agenda de trabalho seja executada e a frequência com que a agenda de trabalho se repete em meses. Por exemplo, se desejar que a agenda de trabalho seja executada no 15º dia do mês a cada dois meses, selecione **Dia** e digite "15" na primeira caixa e "2" na segunda caixa. Observe que o maior número permitido na segunda caixa é "99".  
  
                    -   Se você selecionar **O**, selecione o dia específico da semana no mês que você deseja que a agenda de trabalho seja executada e a frequência com que a agenda de trabalho se repete em meses. Por exemplo, se você desejar que a agenda de trabalho seja executada no último dia da semana do mês a cada dois meses, selecione **Dia**, selecione **último** na primeira lista e **dia da semana** na segunda lista e depois digite “2” na última caixa. Você também pode selecionar **primeiro**, **segundo**, **terceiro**ou **quarto**, bem como dias específicos da semana (por exemplo: domingo ou quarta-feira) nas primeiras duas listas. Observe que o maior número permitido na última caixa é "99".  
  
            2.  Em **Frequência diária**, especifique a frequência com que a agenda de trabalho se repete no dia da execução da agenda de trabalho:  
  
                -   Se você selecionar **Ocorre uma vez às**, digite a hora específica do dia em que a agenda de trabalho deve ser executada na caixa **Ocorre uma vez às** . Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
                -   Se você selecionar **Ocorre a cada**, especifique a frequência com que a agenda de trabalho é executada durante o dia escolhido em **Frequência**. Por exemplo, se você desejar que o agendamento de trabalho se repita a cada 2 horas durante o dia em que é executado, selecione **Ocorre a cada**, digite "2" na primeira caixa e selecione **hora(s)** na lista. Nessa lista, você pode selecionar também **minuto(s)** e **segundo(s)**. Observe que o maior número permitido na primeira caixa é "100".  
  
                     Na caixa **Iniciando às** , digite a hora em que a agenda de trabalho deve começar a ser executada. Na caixa **Terminando às** , digite a hora em que a agenda de trabalho deve parar de se repetir. Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
            3.  Em **Duração**, em **Data de início**, digite a data que você deseja que a agenda de trabalho inicie a execução. Selecione **Data de término** ou **Nenhuma data de término** para indicar quando a execução da agenda de trabalho deve parar. Se você selecionar **Data de término**, digite a data em que você deseja que a execução da agenda de trabalho pare.  
  
        5.  Se você selecionar **Uma Vez**, em **Ocorrência única**, na caixa **Data** , insira a data em que o agendamento de trabalho será executado. Na caixa **Hora** , digite a hora em que a agenda de trabalho será executada. Digite a hora, os minutos e os segundos do dia, bem como AM ou PM.  
  
        6.  Em **Resumo**, em **Descrição**, verifique se todas as configurações da agenda de trabalho estão corretas.  
  
        7.  Clique em **OK**.  
  
    6.  Clique em **Avançar**.  
  
6.  Na página **Selecionar Servidores de Destino** , selecione os servidores nos quais você deseja executar o plano de manutenção. Essa página só é visível em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão configuradas como servidores mestre.  
  
    > **OBSERVAÇÃO:** para criar um plano de manutenção multisservidor, é necessário configurar um ambiente multisservidor contendo um servidor mestre e um ou mais servidores de destino e o servidor local deve estar configurado como um servidor mestre. Em ambientes multisservidor, essa página exibe o servidor mestre **(local)** e todos os servidores de destino correspondentes.  
  
7.  Na página **Selecionar Tarefas de Manutenção** , selecione uma ou mais tarefas de manutenção que devem ser adicionadas ao plano. Quando tiver selecionado todas as tarefas necessárias, clique em **Avançar**.  
  
    > **OBSERVAÇÃO:** as tarefas selecionadas aqui determinarão quais páginas deverão ser preenchidas após a página **Selecionar Ordem da Tarefa de Manutenção** abaixo.  
  
8.  Na página **Selecionar Ordem da Tarefa de Manutenção**, selecione uma tarefa e clique em **Mover para Cima...** ou em **Mover para Baixo...** para alterar sua ordem de execução. Ao concluir ou se você estiver satisfeito com a ordem atual das tarefas, clique em **Avançar**.  
  
    > **OBSERVAÇÃO:** se você selecionou **Agendamentos separados para cada tarefa** na página **Selecionar Propriedades do Plano** acima, não será possível alterar a ordem das tarefas de manutenção nessa página.  
  
## <a name="define-database-check-integrity-checkdb"></a>Definir integridade da verificação do banco de dados (CHECKDB)  
  
 Na página **Definir Tarefa Integridade da Verificação do Banco de Dados** , escolha os bancos de dados nos quais a alocação e a integridade estrutural de tabelas de usuário e do sistema, e também índices, serão verificados. Ao executar a instrução `DBCC CHECKDB`[!INCLUDE[tsql](../../includes/tsql-md.md)] , essa tarefa garante que todos os problemas de integridade com o banco de dados sejam relatados, permitindo assim que eles sejam tratados posteriormente por um administrador do sistema ou proprietário do banco de dados. Para obter mais informações, consulte [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)Quando terminar, clique em **Avançar**.  
  
As opções a seguir estão disponíveis nesta página.  
  
 Lista**Bancos de Dados**   
 Especifique os bancos de dados afetados por essa tarefa.  
  
 -  **Todos os bancos de dados**  
  
Gere um plano de manutenção que execute essa tarefa com todos os bancos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto **tempdb**.  
  
**Bancos de dados do sistema**  
  
  - Gere um plano de manutenção que execute essa tarefa com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto **tempdb** e bancos de dados criados pelo usuário.  
  
 **Todos os bancos de dados de usuários (exceto mestre, modelo, msdb, tempdb)**  
  
 - Gere um plano de manutenção que execute essa tarefa em todos os bancos de dados criados por usuários. Nenhuma tarefa de manutenção é executada com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Estes bancos de dados**  
  
  - Gera um plano de manutenção que execute essa tarefa somente nos bancos de dados selecionados. Pelo menos um banco de dados da lista deverá ser selecionado se esta opção for escolhida.  
  
Caixa de seleção**Incluir índices**   
 - Verifique a integridade de todas as páginas de índice, assim como das páginas de dados de tabela.  
  
**Somente físico**  
 - Limita a verificação à integridade da estrutura física da página, cabeçalhos de registros e a consistência da alocação do banco de dados. O uso dessa opção pode reduzir o tempo de execução de DBCC CHECKDB em bancos de dados grandes e é recomendado para uso frequente em sistemas de produção.  
  
**Tablock**  
 - Faz com que DBCC CHECKDB obtenha bloqueios em vez de usar um instantâneo do banco de dados interno. Isso inclui um bloqueio exclusivo (X) de curto prazo no banco de dados. O uso dessa opção pode ajudar o DBCC CHECKDB a ser executado com mais rapidez em um banco de dados sob carga pesada, mas reduz a simultaneidade disponível no banco de dados durante a execução do DBCC CHECKDB.  
  
## <a name="define-database-shrink-tasks"></a>Definir tarefas de redução de bancos de dados  
  
1.  Na página **Definir Tarefa Reduzir Banco de Dados** , crie uma tarefa que tente reduzir o tamanho dos bancos de dados selecionados usando a instrução `DBCC SHRINKDATABASE` com a opção `NOTRUNCATE` ou `TRUNCATEONLY` . Para obter mais informações, consulte [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md). Ao concluir, clique em **Avançar**.  
  
    > **AVISO!** Os dados movidos para reduzir um arquivo podem ser dispersos para qualquer local disponível no arquivo. Isso provoca uma fragmentação do índice e pode reduzir a velocidade do desempenho de consultas que pesquisam um intervalo do índice. Para eliminar a fragmentação, considere a recompilação dos índices no arquivo após a redução.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     Lista**Bancos de Dados**   
     Especifique os bancos de dados afetados por essa tarefa. Consulte a etapa 9 acima para obter mais informações sobre as opções disponíveis nessa lista.  
  
     Caixa**Reduzir o banco de dados quando ele ultrapassar**   
     Especifique o tamanho em megabytes que faz a tarefa ser executada.  
  
     Caixa**Quantidade de espaço livre restante após redução**   
     Parar a redução quando o espaço livre nos arquivos de banco de dados alcançar esse tamanho (como porcentagem).  
  
     **Reter espaço livre em arquivos de banco de dados**  
     O banco de dados é condensado para páginas contíguas, mas elas não são desalocadas e os arquivos de banco de dados não são reduzidos. Use essa opção se quiser que o banco de dados expanda novamente e não desejar realocar espaço. Com essa opção, os arquivos de banco de dados não são reduzidos ao máximo possível. A opção NOTRUNCATE é usada.  
  
     **Retornar espaço livre para o sistema operacional**  
     O banco de dados é condensado para páginas contíguas e as páginas são liberadas de volta ao sistema operacional para serem usadas por outros programas. A opção TRUNCATEONLY é usada. Essa é a opção padrão.  
  
## <a name="define-the-index-tasks"></a>Definir as tarefas de índice  
  
1.  Na página **Definir Tarefa Reorganizar Índice** , selecione os servidores nos quais você moverá páginas de índice para uma ordem de pesquisa mais eficiente. Esta tarefa usa a instrução `ALTER INDEX ... REORGANIZE`. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md). Ao concluir, clique em **Avançar**.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     Lista**Bancos de Dados**   
     Especifique os bancos de dados afetados por essa tarefa. Consulte a etapa 9 acima para obter mais informações sobre as opções disponíveis nessa lista.  
  
     Lista**Objeto**   
     Limite a lista **Seleção** para exibir tabelas, exibições ou ambas. Essa lista estará disponível somente se um único banco de dados for escolhido na lista **Bancos de Dados** acima.  
  
     Lista**Seleção**   
     Especifique as tabelas ou índices afetados por esta tarefa. Não disponível quando **Tabelas e Exibições** estiver selecionado na caixa Objeto.  
  
     Caixa de seleção**Compactar objetos grandes**   
     Desaloque espaço em tabelas e exibições quando possível. Esta opção usa `ALTER INDEX ... LOB_COMPACTION = ON`.  
  
2.  Na página **Definir Tarefa Recompilar Índice** , selecione o banco de dados ou os bancos de dados nos quais vários índices serão recriados. Esta tarefa usa a instrução `ALTER INDEX ... REBUILD PARTITION`. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).) Ao concluir, clique em **Avançar**.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     Lista**Bancos de Dados**   
     Especifique os bancos de dados afetados por essa tarefa. Consulte a etapa 9 acima para obter mais informações sobre as opções disponíveis nessa lista.  
  
     Lista**Objeto**   
     Limite a lista **Seleção** para exibir tabelas, exibições ou ambas. Essa lista estará disponível somente se um único banco de dados for escolhido na lista **Bancos de Dados** acima.  
  
     Lista**Seleção**   
     Especifique as tabelas ou índices afetados por esta tarefa. Não disponível quando **Tabelas e Exibições** estiver selecionado na caixa Objeto.  
  
     Área**Opções de espaço livre**   
     Apresenta opções para aplicar o fator de preenchimento a índices e tabelas.  
  
     **Espaço livre padrão por página**  
     Reorganiza as páginas com a quantidade padrão de espaço livre. Isso descartará os índices nas tabelas no banco de dados e os recriará com o fator de preenchimento especificado quando os índices foram criados. Essa é a opção padrão.  
  
     Caixa**Alterar espaço livre por página para**   
     Descarta os índices nas tabelas no banco de dados e recria-os com um fator de preenchimento novo, calculado automaticamente, reservando a quantidade especificada de espaço livre nas páginas de índice. Quanto maior a porcentagem, mais espaço livre será reservado nas páginas de índice e maior ficará o índice. Os valores válidos são de 0 a 100. Usa a opção `FILLFACTOR` .  
  
     Área**Opções avançadas**   
     Apresenta opções adicionais para classificar índices e reindexar.  
  
     Caixa de seleção**Classificar resultados no tempdb**   
     Usa a opção `SORT_IN_TEMPDB` , que determina onde são armazenados temporariamente os resultados intermediários de classificação, gerados durante a criação do índice. Se uma operação de classificação não for necessária, ou se a classificação puder ser executada na memória, a opção `SORT_IN_TEMPDB` será ignorada.  
  
     Caixa de seleção**Preenchimento de Índice**   
     Usa a opção `PAD_INDEX` .  
  
     Caixa de seleção**Manter o índice online enquanto estiver reindexando**   
     Usa a opção `ONLINE` , que permite o acesso dos usuários aos dados de índice clusterizado ou da tabela subjacente e todos os índices não clusterizados associados durante as operações de índice. A seleção dessa opção ativa opções adicionais para a recriação de índices que não permitem recriações online: **Não recompilar índices** e **Recompilar índices offline**.  
  
     A seleção dessa opção também ativa Baixa Prioridade Usada, que usa a opção `WAIT_AT_LOW_PRIORITY` . As operações de recriação do índice online aguardará bloqueios de baixa prioridade por `MAX_DURATION` minutos, permitindo que outras operações continuem enquanto a operação de criação de índice online estiver aguardando.  
  
    > **OBSERVAÇÃO:** as operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
     Caixa de seleção**MAXDOP**   
     Substitui a opção de configuração de grau máximo de paralelismo de sp_configure para DBCC CHECKDB. Para obter mais informações, veja [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
#### <a name="define-the-update-statistics-task"></a>Definir a tarefa de atualização de estatísticas  
  
1.  Na página **Definir Tarefa Atualizar Estatísticas** , defina os bancos de dados nos quais as estatísticas de índice e tabela serão atualizadas. Esta tarefa usa a instrução `UPDATE STATISTICS`. Para obter mais informações, consulte [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md) Quando terminar, clique em **Avançar**  
  
     As opções a seguir estão disponíveis nesta página.  
  
     Lista**Bancos de Dados**   
     Especifique os bancos de dados afetados por essa tarefa. Consulte a etapa 9 acima para obter mais informações sobre as opções disponíveis nessa lista.  
  
     Lista**Objeto**   
     Limite a lista **Seleção** para exibir tabelas, exibições ou ambas. Essa lista estará disponível somente se um único banco de dados for escolhido na lista **Bancos de Dados** acima.  
  
     Lista**Seleção**   
     Especifique as tabelas ou índices afetados por esta tarefa. Não disponível quando **Tabelas e Exibições** estiver selecionado na caixa Objeto.  
  
     **Todas as estatísticas existentes**  
     Atualize as estatísticas de colunas e índices.  
  
     **Somente estatísticas de coluna**  
     Atualiza apenas as estatísticas de coluna. Usa a opção `WITH COLUMNS` .  
  
     **Somente estatísticas do índice**  
     Só atualiza estatísticas do índice. Usa a opção `WITH INDEX` .  
  
     **Tipo de exame**  
     Tipo de exame usado para coletar estatísticas atualizadas.  
  
     **Exame completo**  
     Lê todas as linhas na tabela ou exibição para coletar as estatísticas.  
  
     **Amostra por**  
     Especifique a porcentagem da tabela ou exibição indexada ou o número de linhas de amostragem ao coletar estatísticas de tabelas ou exibições maiores.  
  
#### <a name="define-the-history-cleanup-task"></a>Definir a tarefa de limpeza do histórico  
  
1.  Na página **Definir Tarefa Limpeza do Histórico** , defina os bancos de dados nos quais você deseja descartar o histórico de tarefas antigo. Essa tarefa usa as instruções `EXEC sp_purge_jobhistory`, `EXEC sp_maintplan_delete_log`e `EXEC sp_delete_backuphistory` para remover informações de histórico das tabelas do **msdb** . Ao concluir, clique em **Avançar**.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     **Selecione os dados históricos a serem excluídos**  
     Escolha o tipo de dados de tarefa a serem excluídos/  
  
     **Histórico de backup e restauração**  
     A retenção de registros de quando foram criados backups recentes pode ajudar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criar um plano de recuperação quando você desejar restaurar um banco de dados. O período de retenção deve ser pelo menos a frequência de backups de banco de dados completos.  
  
     **Histórico de trabalho do SQL Server Agent**  
     Esse histórico pode ajudar a solucionar problemas de trabalhos com falha ou a determinar por que ações de banco de dados ocorreram.  
  
     **Histórico do Plano de Manutenção**  
     Esse histórico pode ajudar a solucionar problemas de trabalhos de plano de manutenção com falha ou a determinar por que ações de banco de dados ocorreram.  
  
     **Remover dados históricos com mais de**  
     Especifique a idade de itens que deseja excluir. Você pode especificar **Hora(s)**, **Dia(s)**, **Semana(s)** (o padrão), **Mês(es)**, ou **Ano(s)**  
  
#### <a name="define-the-execute-agent-job-task"></a>Definir a tarefa de execução de trabalho do Agent  
  
1.  Na página **Definir Tarefa Executar Trabalho do Agent** , em **Trabalhos do SQL Server Agent disponíveis**, escolha os trabalhos a serem executados. Essa opção não estará disponível se você não tiver nenhum trabalho de SQL Agent. Esta tarefa usa a instrução `EXEC sp_start_job`. Para obter mais informações, consulte [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)Quando terminar, clique em **Avançar**.  
  
#### <a name="define-backup-tasks"></a>Definir tarefas de backup  
  
1.  Na página **Definir Tarefa Backup de Banco de Dados (Completo)** , selecione os bancos de dados nos quais deve ser executado um backup completo. Esta tarefa usa a instrução `BACKUP DATABASE`. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md). Ao concluir, clique em **Avançar**.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     Lista**Tipo de Backup**   
     Exibe o tipo de backup a ser executado. Esse item é somente leitura.  
  
     Lista**Bancos de Dados**   
     Especifique os bancos de dados afetados por essa tarefa. Consulte a etapa 9 acima para obter mais informações sobre as opções disponíveis nessa lista.  
  
     **Componente de backup**  
     Selecione **Banco de dados** para fazer o backup de todo o banco de dados. Selecione **Arquivo e grupos de arquivos** para fazer o backup de apenas uma parte do banco de dados. Se selecionado, forneça o nome do arquivo ou do grupo de arquivos. Quando vários bancos de dados são selecionados na caixa **Bancos de dados** , especifique apenas **Bancos de dados** para **Componentes de backup**. Para executar backups de arquivo ou grupo de arquivos, crie uma tarefa para cada banco de dados. Essas opções estarão disponíveis somente se um único banco de dados for escolhido na lista **Bancos de Dados** acima.  
  
     Caixa de seleção**O conjunto de backup vai expirar**   
     Especifica quando o conjunto de backup desse backup pode ser substituído. Selecione **Após** e insira um número de dias para a validade ou selecione **Em** e insira a data de validade. Essa opção será desabilitada se a opção **URL** for selecionada como o destino de backup.  
  
     **Fazer backup em**  
     Especifica o meio no qual deve ser feito o backup do banco de dados. Selecione **Disco**, **Fita**ou **URL**. Somente dispositivos de fita anexados ao computador que contém o banco de dados estão disponíveis.  
  
     **Backup de banco de dados por um ou mais arquivos**  
     Clique em **Adicionar** para abrir a caixa de diálogo **Selecionar Destino do Backup** . Essa opção será desabilitada se a opção URL for selecionada como o destino de backup.  
  
     Clique em **Remover** para remover um arquivo da caixa.  
  
     Clique em **Conteúdo** para ler o cabeçalho de arquivo e exibir os conteúdos de backup atuais do arquivo.  
  
     Caixa de diálogo**Selecionar Destino do Backup**   
     Selecione o arquivo, a unidade de fita ou o dispositivo de backup para o destino de backup. Essa opção será desabilitada se a opção URL for selecionada como o destino de backup.  
  
     Lista**Se houver arquivos de backup**   
     Especifique como tratar backups existentes. Selecione **Anexar** para adicionar os backups novos depois de qualquer backup existente no arquivo ou na fita. Selecione **Substituir** para remover o conteúdo antigo de um arquivo ou fita e substituir por esse backup novo.  
  
     **Crie um arquivo de backup para cada banco de dados**  
     Crie um arquivo de backup no local especificado na caixa de pasta. Um arquivo é criado para cada banco de dados selecionado. Essa opção será desabilitada se a opção URL for selecionada como o destino de backup.  
  
     Caixa de seleção**Criar um subdiretório para cada banco de dados**   
     Crie um subdiretório no diretório da unidade de disco especificada que contém o backup de banco de dados para cada banco de dados cujo backup está sendo executado como parte do plano de manutenção.  
  
    > **IMPORTANTE:** O subdiretório herdará permissões do diretório pai. Restrinja permissões para evitar acesso não autorizado.  
  
     Caixa**Pasta**   
     Especifique a pasta para os arquivos de banco de dados automaticamente criados. Essa opção será desabilitada se a opção URL for selecionada como o destino de backup.  
  
     **CREDENCIAL DO SQL**  
     Selecione uma Credencial do SQL usada para autenticar o Armazenamento do Windows Azure. Se você não tiver uma Credencial existente do SQL que possa usar, clique no botão **Criar** para criar uma nova Credencial do SQL.  
  
    > **IMPORTANTE:** A caixa de diálogo que é aberta quando você clica em **Criar** exige um certificado de gerenciamento ou o perfil da publicação para a assinatura. Se você não tiver acesso ao certificado de gerenciamento ou perfil de publicação, poderá criar uma credencial de SQL especificando o nome da conta de armazenamento e as informações da chave de acesso usando Transact-SQL ou SQL Server Management Studio. Consulte o código de exemplo no tópico [Criar uma credencial](../../relational-databases/backup-restore/sql-server-backup-to-url.md#credential) para criar uma credencial usando Transact-SQL. Como alternativa, usando o SQL Server Management Studio, na instância do mecanismo de banco de dados, clique com o botão direito do mouse em **Segurança**, selecione **Novo**e **Credencial**. Especifique o nome da conta de armazenamento para **Identidade** e a chave de acesso no campo **Senha** .  
  
     **Contêiner de armazenamento do Azure**  
     Especifique o nome do contêiner de armazenamento do Windows Azure  
  
     **Prefixo da URL:**  
     Gerado automaticamente com base nas informações da conta de armazenamento armazenadas na Credencial do SQL e o nome do contêiner de armazenamento do Azure que você especificou. É recomendável não editar as informações neste campo, a menos que você esteja usando um domínio que use um formato diferente de **\<conta de armazenamento>.blob.core.windows.net**.  
  
     Caixa**Extensão do arquivo de backup**   
     Especifique a extensão a ser usada para os arquivos de backup. O padrão é .bak.  
  
     Caixa de seleção**Verificar integridade do backup**   
     Verifique se o conjunto de backup está completo e se todos os volumes estão legíveis.  
  
     Caixa de seleção**Executar soma de verificação**   
     Verifique cada página para soma de verificação e página interrompida, se estiver habilitado e disponível, e irá gera uma soma de verificação para o backup inteiro.  
  
     Caixa de seleção**Continuar se houver erro**   
     Instrui BACKUP a continuar apesar de encontrar erros como somas de verificação inválidas ou páginas interrompidas.  
  
     **Criptografia de backup**  
     Para criar um backup criptografado, marque a caixa de seleção **Criptografar backup** . Selecione um algoritmo de criptografia a ser usado na etapa de criptografia e forneça um Certificado ou uma Chave assimétrica de uma lista de certificados ou chaves assimétricas existentes. Os algoritmos de criptografia disponíveis são:  
  
    -   AES 128  
  
    -   AES 192  
  
    -   AES 256  
  
    -   Triple DES  
  
     A opção de criptografia estará desabilitada se você optou por anexar ao conjunto de backup existente.  
  
     É prática recomendada fazer backup do certificado ou das chaves e armazená-los em um local diferente do backup que você criptografou.  
  
     Há suporte somente para as chaves que residem no EKM (Gerenciamento Extensível Chaves).  
  
     caixa de seleção**Tamanho do bloco** , lista  
  
     Especifica o tamanho do bloco físico, em bytes. Normalmente, essa opção afeta o desempenho durante a gravação em dispositivos de fita, matrizes RAID ou SAN.  
  
     caixa de seleção**Tamanho máximo de transferência** , lista  
  
     Especifica a maior unidade de transferência em bytes a ser usada entre a mídia de backup e o SQL Server.  
  
     Lista**Definir compactação de backup**    
     Em [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou versões posteriores), selecione um dos seguintes valores [de compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) :  
  
    |||  
    |-|-|  
    |**Usar a configuração padrão do servidor**|Clique para usar o padrão do nível de servidor. Esse padrão é definido pela opção de configuração do servidor **padrão de compactação de backup** . Para obter informações sobre como exibir a configuração atual dessa opção, consulte [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
    |**Compactar backup**|Clique em compactar backup, independentemente do padrão do nível do servidor.<br /><br /> **\*\* Importante \*\*** Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, convém criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo Administrador de Recursos. Para obter mais informações, consulte [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).|  
    |**Não compactar o backup**|Clique em criar um backup não compactado, independentemente do padrão do nível do servidor.|  
  
2.  Na página **Definir Tarefa de Backup de Banco de Dados (Diferencial)** , selecione o banco de dados ou os bancos de dados dos quais deve ser executado um backup parcial. Consulte lista de definições na etapa 16 acima para obter mais informações sobre as opções disponíveis nessa página. Esta tarefa usa a instrução `BACKUP DATABASE ... WITH DIFFERENTIAL`. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  Ao concluir, clique em **Avançar**.  
  
3.  Na página **Definir Tarefa de Backup de Banco de Dados (Log de Transações)** , selecione o banco de dados ou os bancos de dados dos quais deve ser executado um backup de um log de transações. Consulte lista de definições na etapa 16 acima para obter mais informações sobre as opções disponíveis nessa página. Esta tarefa usa a instrução `BACKUP LOG`. Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md). Ao concluir, clique em **Avançar**.  
  
#### <a name="define-maintenance-cleanup-tasks"></a>Definir tarefas de limpeza de manutenção  
  
1.  Na página **Definir Tarefa Limpeza de Manutenção** , especifique os tipos de arquivos que devem ser excluídos como parte do plano de manutenção, inclusive relatórios de texto criados por planos de manutenção e arquivos de backup de banco de dados. Esta tarefa usa a instrução `EXEC xp_delete_file` . Ao concluir, clique em **Avançar**.  
  
    > **IMPORTANTE:** Essa tarefa não exclui automaticamente os arquivos nas subpastas do diretório especificado. Essa precaução reduz a possibilidade de um ataque mal-intencionado que use a tarefa de Limpeza de Manutenção para excluir arquivos. Se quiser excluir arquivos em subpastas de primeiro nível, você deverá selecionar **Incluir subpastas de primeiro nível**.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     **Excluir arquivos do seguinte tipo**  
     Especifique o tipo de arquivos que devem ser excluídos.  
  
     **Arquivos de backup**  
     Exclua arquivos de backup de banco de dados.  
  
     **Relatórios de texto do Plano de Manutenção**  
     Exclua relatórios de texto de planos de manutenção executados anteriormente.  
  
     **Local do arquivo**  
     Especifique o caminho dos arquivos que devem ser excluídos.  
  
     **Excluir arquivo específico**  
     Exclua o arquivo específico fornecido na caixa de texto **Nome do arquivo** .  
  
     **Pesquisar pasta e excluir arquivos com base em uma extensão**  
     Exclua todos os arquivos com a extensão especificada na pasta especificada. Use para excluir vários arquivos de uma vez, como todos os arquivos de backup com a extensão .bak, na pasta Terça-feira.  
  
     Caixa**Pasta**   
     Caminho e nome da pasta que contém os arquivos a serem excluídos.  
  
     Caixa**Extensão do arquivo**   
     Forneça a extensão de arquivo dos arquivos a serem excluídos. Para excluir vários arquivos de uma vez, como todos os arquivos de backup com a extensão .bak na pasta Terça-feira, especifique .bak.  
  
     Caixa de seleção**Incluir subpastas de primeiro nível**   
     Exclua arquivos com a extensão especificada em **Extensão de arquivo** de subpastas de primeiro nível sob a pasta especificada em **Pasta**.  
  
     Caixa de seleção**Excluir arquivos com base na idade do arquivo em tempo de execução da tarefa**   
     Especifique a idade mínima dos arquivos que você deseja excluir fornecendo um número e unidade de tempo na caixa **Excluir arquivos com idade acima de** .  
  
     **Excluir arquivos com idade acima de**  
     Especifique a idade mínima dos arquivos que você deseja excluir, fornecendo um número e a unidade de tempo (**Hora**, **Dia**, **Semana**, **Mês**ou **Ano**). Arquivos com idade acima do período especificado serão excluídos.  
  
#### <a name="select-report-options"></a>Selecionar Opções de Relatório  
  
1.  Na página **Selecionar Opções de Relatório** , selecione as opções para salvar ou distribuir um relatório das ações do plano de manutenção. Esta tarefa usa a instrução `EXEC sp_notify_operator`. Para obter mais informações, consulte [sp_notify_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-notify-operator-transact-sql.md). Quando terminar, clique em **Avançar**.  
  
     As opções a seguir estão disponíveis nesta página.  
  
     Caixa de seleção**Gravar relatório em um arquivo de texto**   
     Salve o relatório em um arquivo.  
  
     Caixa**Local da pasta**   
     Especifique o local do arquivo que conterá o relatório.  
  
     Caixa de seleção**Enviar relatório por email**   
     Envia um email quando uma tarefa falha. Para usar essa tarefa é necessário ter o Database Mail habilitado e configurado corretamente com MSDB como um Banco de dados do host de correio e ter um operador do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com um endereço de email válido.  
  
     **Operador do agente**  
     Especifique o destinatário do email.  
  
     **Perfil de email**  
     Especifique o perfil que define o remetente do email.  
  
#### <a name="complete-the-wizard"></a>Concluir o Assistente  
  
1.  Na página **Concluir o Assistente** , verifique as opções escolhidas nas páginas anteriores e clique em **Concluir**.  
  
2.  Na página **Progresso do Assistente de Manutenção** , monitore as informações de status das ações do Assistente de Plano de Manutenção. Dependendo das opções selecionadas no assistente, a página de progresso pode conter uma ou várias ações. A caixa superior exibe o status geral do assistente e o número de mensagens de status, erro e aviso que ele recebeu.  
  
     As opções a seguir estão disponíveis na página **Progresso do Assistente de Manutenção** :  
  
     **Detalhes**  
     Fornece a ação, status e qualquer mensagem retornada pela ação executada pelo assistente.  
  
     **Ação**  
     Especifica o tipo e o nome de cada ação.  
  
     **Status**  
     Indica se a ação do assistente retornou como um todo o valor de **Êxito** ou de **Falha**.  
  
     **Mensagem**  
     Fornece qualquer mensagem de aviso ou erro retornada pelo processo.  
  
     **Relatório**  
     Cria um relatório contendo os resultados do Assistente para Criar Partição. As opções são **Exibir Relatório**, **Salvar Relatório no Arquivo**, **Copiar Relatório na Área de Transferência**e **Enviar Relatório como Email**.  
  
     **Exibir Relatório**  
     Abre a caixa de diálogo **Exibir Relatório** , que contém um relatório de texto do progresso do Assistente para Criar Partições.  
  
     **Salvar Relatório no Arquivo**  
     Abre a caixa de diálogo **Salvar Relatório Como** .  
  
     **Copiar Relatório na Área de Transferência**  
     Copia os resultados do relatório de progresso do assistente na Área de transferência.  
  
     **Enviar Relatório como Email**  
     Copia os resultados do relatório de progresso do assistente para uma mensagem de email.  
  
  

