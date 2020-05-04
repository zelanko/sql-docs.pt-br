---
title: Atualizar bancos de dados usando o Assistente de Ajuste de Consulta
ms.custom: seo-dt-2019
ms.date: 02/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
- query profiling
- lightweight query profiling
- lightweight profiling
ms.assetid: 07f8f594-75b4-4591-8c29-d63811e7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 3113caec4026547fcf2dca940a3908f64b6efa44
ms.sourcegitcommit: 69f93dd1afc0df76c3b4d9203adae0ad7dbd7bb2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82598742"
---
# <a name="upgrading-databases-by-using-the-query-tuning-assistant"></a>Atualizando bancos de dados usando o Assistente de Ajuste de Consulta
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Ao migrar de versões mais antigas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou mais recente e [atualizar o nível de compatibilidade do banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) para o mais recente disponível, uma carga de trabalho poderá ser exposta ao risco de regressão de desempenho. Isso também é possível em um grau menor ao atualizar entre o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e qualquer versão mais recente.

Começando com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], e a cada nova versão, todas as alterações do otimizador de consulta são restritas ao último nível de compatibilidade do banco de dados, portanto, os planos de execução não são alterados diretamente no ponto de atualização, mas sim quando um usuário altera a opção do banco de dados `COMPATIBILITY_LEVEL` para a versão mais recente disponível. Para obter mais informações sobre as alterações do otimizador de consulta introduzidas no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], confira [Estimador de cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md). Para saber mais sobre os níveis de compatibilidade e como eles podem afetar as atualizações, confira [Níveis de compatibilidade e atualizações do Mecanismo de Banco de Dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades).

Essa funcionalidade associada fornecida pelo nível de compatibilidade do banco de dados, em combinação com o Repositório de Consultas oferece um excelente nível de controle sobre o desempenho da consulta no processo de atualização quando a atualização segue o fluxo de trabalho recomendado, mostrado abaixo. Para obter mais informações sobre o fluxo de trabalho recomendado para atualizar o nível de compatibilidade, confira [Alterar o modo de compatibilidade do banco de dados e usar o Repositório de Consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). 

![Fluxo de trabalho de atualização de banco de dados recomendado usando o Repositório de Consultas](../../relational-databases/performance/media/query-store-usage-5.png "Fluxo de trabalho de atualização de banco de dados recomendado usando o Repositório de Consultas") 

Esse controle sobre as atualizações foi ainda mais aprimorado no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], no qual o [Ajuste Automático](../../relational-databases/automatic-tuning/automatic-tuning.md) foi introduzido permitindo automatizar a última etapa no fluxo de trabalho recomendado acima.

Começando com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18, o novo recurso **QTA (Assistente de Ajuste de Consulta)** orientará os usuários pelo fluxo de trabalho recomendado para manter a estabilidade do desempenho durante as atualizações para as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais recentes, conforme documentado na seção *Manter a estabilidade do desempenho durante a atualização para o SQL Server mais recente* dos [Cenários de uso do Repositório de Consultas](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade). No entanto, o QTA não é revertido para um plano em bom estado anteriormente conhecido, como visto na última etapa do fluxo de trabalho recomendado. Em vez disso, o QTA vai rastrear todas as regressões encontradas na exibição [**Consultas Regredidas** do Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed) e iterar por meio de possíveis permutações das variações do modelo do otimizador aplicável para que um plano novo e melhor possa ser gerado.

> [!IMPORTANT]
> O QTA não gera a carga de trabalho do usuário. Ao executar o QTA em um ambiente que não seja usado pelos seus aplicativos, verifique se ainda é possível executar uma carga de trabalho de teste representativa no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de destino por outros meios. 

## <a name="the-query-tuning-assistant-workflow"></a>O fluxo de trabalho do Assistente de Ajuste de Consulta
O ponto de partida do QTA supõe que um banco de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja movido (por [CREATE DATABASE... FOR ATTACH](../..//relational-databases/databases/attach-a-database.md) ou [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)) para uma versão mais recente do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], e o nível de compatibilidade do banco de dados antes da atualização não será alterado imediatamente. O QTA orientará pelas etapas a seguir:
1.  Configure o Repositório de Consultas de acordo com as configurações recomendadas de duração da carga de trabalho (em dias) definidas pelo usuário. Pense em uma duração de carga de trabalho que corresponda ao seu ciclo comercial típico.
2.  Solicite o início da carga de trabalho necessária para que esse Repositório de Consultas possa coletar uma linha de base de dados de carga de trabalho (se ainda não houver nenhum disponível).
3.  Atualize para o nível de compatibilidade do banco de dados de destino escolhido pelo usuário.
4.  Solicite que uma segunda leva de dados de carga de trabalho seja coletada para a detecção de regressão e de comparação.
5.  Itere por meio das regressões encontradas na exibição [**Consultas Regredidas** do Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed), experimente a coleta de estatísticas de runtime sobre possíveis permutações de variações de modelo do otimizador aplicável e meça o resultado. 
6.  Relate as melhorias medidas e, opcionalmente, permita que essas alterações persistam usando [guias de plano](../../relational-databases/performance/plan-guides.md).

Para obter mais informações sobre como anexar um banco de dados, confira [Anexar e desanexar bancos de dados](../../relational-databases/databases/database-detach-and-attach-sql-server.md#AttachDb).

Veja abaixo como o QTA basicamente apenas muda as últimas etapas do fluxo de trabalho recomendado para atualizar o nível de compatibilidade usando o Repositório de Consultas mostrado acima. Em vez de oferecer a opção de escolher entre o plano de execução ineficiente no momento e o último plano de execução eficiente conhecido, o QTA apresenta opções de ajuste específicas das consultas regredidas selecionadas para a criação de um novo estado aprimorado com planos de execução ajustados.

![Fluxo de trabalho de atualização do banco de dados recomendado usando o QTA](../../relational-databases/performance/media/qta-usage.png "Fluxo de trabalho de atualização do banco de dados recomendado usando o QTA")

### <a name="qta-tuning-internal-search-space"></a>Espaço de pesquisa interno do Ajuste do QTA
O QTA é indicado apenas para consultas `SELECT` que podem ser executadas pelo Repositório de Consultas. As consultas parametrizadas são qualificadas quando o parâmetro compilado é conhecido. As consultas que dependem de construções de runtime, como tabelas temporárias ou variáveis de tabela não são qualificadas no momento. 

O QTA é indicado para possíveis padrões de regressões de consulta devido a alterações nas versões [CE (Estimador de Cardinalidade)](../../relational-databases/performance/cardinality-estimation-sql-server.md). Por exemplo, durante a atualização de um banco de dados do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e do nível de compatibilidade do banco de dados 110 para o [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e o nível de compatibilidade do banco de dados 140, algumas consultas podem regredir porque foram projetadas especificamente para funcionar com a versão do CE que existia no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (CE 70). Isso não significa que a reversão do CE 140 para o CE 70 é a única opção. Se apenas uma alteração específica da versão mais recente estiver apresentando a regressão, será possível indicar essa consulta a usar apenas a parte relevante da versão anterior do CE que estava funcionando melhor para a consulta específica, continuando a aproveitar todas as outras melhorias das versões mais recentes do CE. E também permitir que as outras consultas na carga de trabalho que não regrediram se beneficiem das melhorias mais recentes do CE.

Os padrões do CE pesquisados pelo QTA são os seguintes: 
-  **Independência versus Correlação**: se a pressuposição de independência fornecer estimativas melhores para a consulta específica, a dica de consulta `USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES')` fará com que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gere um plano de execução usando a seletividade mínima ao estimar predicados `AND` para os filtros a serem considerados para correlação. Para obter mais informações, confira [Dicas de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint) e [Versões do CE](../../relational-databases/performance/cardinality-estimation-sql-server.md#versions-of-the-ce).
-  **Independência simples versus independência de base**: se uma independência de junção diferente fornecer estimativas melhores para a consulta específica, a dica de consulta `USE HINT ('ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS')` fará com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gere um plano de execução usando a pressuposição de independência simples em vez da pressuposição de independência de base padrão. Para obter mais informações, confira [Dicas de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint) e [Versões do CE](../../relational-databases/performance/cardinality-estimation-sql-server.md#versions-of-the-ce).
-  **Estimativa de cardinalidade fixa da MSTVF (função com valor de tabela de várias instruções)** de 100 linhas versus 1 linha: se o padrão fixo de estimativa de TVFs de 100 linhas não resultar em um plano mais eficiente do que o uso da estimativa fixa de TVFs de 1 linha (correspondente ao padrão do modelo do CE do otimizador de consulta [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] e versões anteriores), a dica de consulta `QUERYTRACEON 9488` será usada para gerar um plano de execução. Para obter mais informações sobre as MSTVFs, confira [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

> [!NOTE]
> Como último recurso, se as dicas com escopo reduzido não estiverem rendendo bons resultados suficientes para os padrões de consulta elegíveis, também será considerado o uso completo do CE 70 usando a dica de consulta `USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')` para gerar um plano de execução.

> [!IMPORTANT]
> Toda dica força determinados comportamentos que poderão ser resolvidos em atualizações futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É recomendado aplicar dicas apenas quando não houver nenhuma outra opção e planejar rever o código com dicas a cada nova atualização. Ao forçar comportamentos, você pode impedir que sua carga de trabalho se beneficie das melhorias introduzidas nas versões mais recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="starting-query-tuning-assistant-for-database-upgrades"></a>Iniciando o Assistente de Ajuste de Consulta para atualizações de banco de dados
O QTA é um recurso baseado em sessão que armazena o estado de sessão no esquema `msqta` do banco de dados de usuário no qual uma sessão é criada pela primeira vez. Várias sessões de ajuste podem ser criadas em um banco de dados individual ao longo do tempo, mas somente uma sessão ativa pode existir para um determinado banco de dados.

### <a name="creating-a-database-upgrade-session"></a>Criando uma sessão de atualização de banco de dados
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o Pesquisador de Objetos e conecte-se a [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2.  Para o banco de dados cujo nível de compatibilidade será atualizado, clique com o botão direito do mouse no nome do banco de dados, selecione **Tarefas**, selecione **Atualizar Banco de Dados** e clique em **Nova Sessão de Atualização do Banco de Dados**.

3.  Na janela do Assistente QTA, são necessárias duas etapas para configurar uma sessão:

    1.  Na janela **Configuração**, configure o Repositório de Consultas para capturar o equivalente a um ciclo comercial completo de dados de carga de trabalho para análise e ajuste. 
        -  Digite a duração esperada da carga de trabalho em dias (o mínimo é 1 dia). Isso será usado para propor configurações recomendadas do Repositório de Consultas para tentar permitir que a linha de base inteira seja coletada. Capturar uma boa linha de base é importante para garantir que todas as consultas regredidas encontradas depois da alteração do nível de compatibilidade do banco de dados possam ser analisadas. 
        -  Defina o nível de compatibilidade do banco de dados de destino pretendido para o banco de dados de usuário, depois que o fluxo de trabalho do QTA for concluído.
        Após a conclusão, clique em **Avançar**.
    
       ![Janela configuração da sessão de atualização do novo banco de dados](../../relational-databases/performance/media/qta-new-session-setup.png "Janela configuração da atualização do novo banco de dados")  
  
    2.  Na janela **Configurações**, duas colunas mostram o estado **Atual** do Repositório de Consultas no banco de dados de destino, bem como as configurações **Recomendadas**. 
        -  As configurações Recomendadas são selecionadas por padrão, mas o clique no botão de opção na coluna Atual aceita as configurações atuais e também permite ajustar melhor a configuração atual do Repositório de Consultas. 
        -  A configuração *Limite de Consulta Obsoleto* proposta é o dobro do número da duração da carga de trabalho esperada em dias. Isso ocorre porque o Repositório de Consultas precisará manter as informações sobre a carga de trabalho de linha de base e a carga de trabalho após a atualização do banco de dados.
        Após a conclusão, clique em **Avançar**.

       ![Janela de configurações de atualização do novo banco de dados](../../relational-databases/performance/media/qta-new-session-settings.png "Janela de configurações de atualização do novo banco de dados")

       > [!IMPORTANT]
       > O *Tamanho Máximo* proposto é um valor arbitrário que pode ser adequado para uma carga de trabalho com tempo curto.   
       > No entanto, saiba que pode não ser suficiente manter informações sobre as cargas de trabalho de linha de base e após a atualização do banco de dados para cargas de trabalho muito intensivas, ou seja, quando muitos planos diferentes podem ser gerados.   
       > Se você puder prever que isso ocorrerá, insira um valor mais alto que seja apropriado.

4.  A janela **Ajuste** conclui a configuração da sessão e instrui sobre as próximas etapas para abrir e prosseguir com a sessão. Após a conclusão, clique em **Concluir**.

    ![Janela de ajuste de atualização do novo banco de dados](../../relational-databases/performance/media/qta-new-session-tuning.png "Janela de ajuste de atualização do novo banco de dados")

> [!NOTE]
> Um possível cenário alternativo é iniciado restaurando um backup de banco de dados do servidor de produção no qual um banco de dados já tenha passado pelo fluxo de trabalho recomendado de atualização de compatibilidade de banco de dados, para um servidor de teste.

### <a name="executing-the-database-upgrade-workflow"></a>Executando o fluxo de trabalho de atualização de banco de dados
1.  Para o banco de dados cujo nível de compatibilidade será atualizado, clique com o botão direito do mouse no nome do banco de dados, selecione **Tarefas**, selecione **Atualizar Banco de Dados** e clique em **Monitorar Sessões**.

2.  A página **gerenciamento de sessão** lista as sessões atuais e antigas do banco de dados no escopo. Selecione a sessão desejada e clique em **Detalhes**.

    > [!NOTE]
    > Se a sessão atual não estiver presente, clique no botão **Atualizar**.   
    
    A lista contém as seguintes informações:
    -  **ID da Sessão**
    -  **Nome da Sessão**: nome gerado pelo sistema composto pelo nome do banco de dados e pela data e hora da criação da sessão.
    -  **Status**: status da sessão (Ativa ou Fechada).
    -  **Descrição**: gerada pelo sistema composta pelo nível de compatibilidade do banco de dados de destino selecionado pelo usuário e número de dias da carga de trabalho do ciclo comercial.
    -  **Hora de início**: a data e a hora em que a sessão foi criada.

    ![Página de Gerenciamento de Sessão do QTA](../../relational-databases/performance/media/qta-session-management.png "Página de Gerenciamento de Sessão do QTA")

    > [!NOTE]
    > **Excluir Sessão** exclui todos os dados armazenados na sessão selecionada.    
    > No entanto, a exclusão de uma sessão fechada **não** exclui nenhum guia de plano já implantado.   
    > Ao excluir uma sessão que implantou guias de plano, você não poderá usar o QTA para reversão.    
    > Nesse caso, pesquise guias de plano usando a tabela de sistema [sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) e exclua manualmente usando [sp_control_plan_guide](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md).    
  
3.  O ponto de entrada para uma nova sessão é a etapa **Coleta de Dados**. 

    > [!NOTE]
    > O botão **Sessões** retorna à página de **gerenciamento de sessão**, deixando a sessão ativa no estado em que se encontra.

    Essa etapa tem três subetapas:

    1.  A **Coleta de dados de linha de base** solicita que o usuário execute o ciclo de carga de trabalho representativo para que o Repositório de Consultas possa coletar uma linha de base. Quando essa carga de trabalho for concluída, marque **Execução de carga de trabalho concluída** e clique em **Avançar**.

        > [!NOTE]
        > A janela do QTA pode ser fechada enquanto a carga de trabalho é executada. Quando você retornar mais tarde para a sessão que permanece no estado ativo, ela será retomada na mesma etapa em que parou. 

        ![Subetapa 1 da Etapa 2 do QTA](../../relational-databases/performance/media/qta-step2-substep1.png "Subetapa 1 da Etapa 2 do QTA")

    2.  **Atualizar banco de dados** solicitará permissão para atualizar o nível de compatibilidade do banco de dados para o destino desejado. Para prosseguir para a próxima subetapa, clique em **Sim**.

        ![Subetapa 2 da etapa 2 do QTA – atualizar o nível de compatibilidade do banco de dados](../../relational-databases/performance/media/qta-step2-substep2-prompt.png "Subetapa 2 da etapa 2 do QTA – atualizar o nível de compatibilidade do banco de dados")

        A página a seguir confirma que o nível de compatibilidade do banco de dados foi atualizado com êxito.

        ![Subetapa 2 da Etapa 2 do QTA](../../relational-databases/performance/media/qta-step2-substep2.png "Subetapa 2 da Etapa 2 do QTA")

    3.  A **Coleta de Dados Observados** solicita que o usuário execute o ciclo de carga de trabalho representativo mais uma vez para que o Repositório de Consultas possa coletar uma linha de base de comparação que será usada para pesquisar oportunidades de otimização. Conforme a carga de trabalho é executada, use o botão **Atualizar** para continuar atualizando a lista de consultas regredidas, caso alguma seja encontrada. Altere o valor de **Consultas a serem mostradas** para limitar o número de consultas exibidas. A ordem da lista é afetada pela **Métrica** (Duração ou CpuTime) e pela **Agregação** (Média é o padrão). Também selecione quantas **Consultas a serem mostradas**. Quando essa carga de trabalho for concluída, marque **Execução de carga de trabalho concluída** e clique em **Avançar**.

        ![Subetapa 3 da Etapa 2 do QTA](../../relational-databases/performance/media/qta-step2-substep3.png "Subetapa 3 da Etapa 2 do QTA")

        A lista contém as seguintes informações:
        -  **ID da Consulta** 
        -  **Texto da Consulta**: instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que pode ser expandida clicando no botão **...** .
        -  **Execuções**: exibe o número de execuções dessa consulta para toda a coleção da carga de trabalho.
        -  **Métrica de Linha de Base**: a métrica selecionada (Duração ou CpuTime) em ms para a coleta de dados de linha de base antes da atualização de compatibilidade do banco de dados.
        -  **Métrica Observada**: a métrica selecionada (Duração ou CpuTime) em ms para a coleta de dados após a atualização de compatibilidade do banco de dados.
        -  **% de Alteração**: porcentagem de alteração da métrica selecionada entre o estado anterior e posterior de atualização de compatibilidade do banco de dados. Um número negativo representa o valor da regressão medida para a consulta.
        -  **Ajustável**: *True* ou *False* dependendo da qualificação da consulta para experimentação.

4.  **Exibir análise** permite selecionar quais consultas devem ser experimentadas e encontrar oportunidades de otimização. O valor **Consultas a serem mostradas** torna-se o escopo das consultas qualificadas para experimentação. Depois que as consultas desejadas forem verificadas, clique em **Avançar** para começar a experimentação.  

    > [!NOTE]
    > As consultas com Ajustável = False não podem ser selecionadas para experimentação.   
 
    > [!IMPORTANT]
    > Um prompt avisa que depois que QTA mudar para a fase de experimentação, não será possível retornar para a página Exibir análise.   
    > Se você não selecionar todas as consultas qualificadas antes de passar para a fase de experimentação, será necessário criar uma sessão mais tarde e repetir o fluxo de trabalho. Isso exige a reinicialização do nível de compatibilidade do banco de dados para o valor anterior.

    ![Etapa 3 do QTA](../../relational-databases/performance/media/qta-step3.png "Etapa 3 do QTA")

5.  **Exibir descobertas** permite selecionar as consultas para implantar a otimização proposta como um guia de plano. 

    A lista contém as seguintes informações:
    -  **ID da Consulta** 
    -  **Texto da Consulta**: instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que pode ser expandida clicando no botão **...** .
    -  **Status**: exibe o estado atual de experimentação para a consulta.
    -  **Métrica de Linha de Base**: a métrica selecionada (Duração ou CpuTime) em ms para a consulta executada na **Subetapa 3 da Etapa 2**, que representa a consulta regredida após a atualização de compatibilidade do banco de dados.
    -  **Métrica Observada**: a métrica selecionada (Duração ou CpuTime) em ms para a consulta após a experimentação, para uma otimização suficientemente boa.
    -  **% de Alteração**: porcentagem de alteração da métrica selecionada entre o estado de experimentação anterior e posterior, que representa o valor da melhoria medida para a consulta com a otimização proposta.
    -  **Opção de Consulta**: link para a dica proposta que melhora a métrica de execução de consulta.
    -  **Pode Implantar**: *True* ou *False*, dependendo se a otimização de consulta proposta pode ser implantada como um guia de plano.

    ![Etapa 4 do QTA](../../relational-databases/performance/media/qta-step4.png "Etapa 4 do QTA")

6.  **Verificação** mostra o status de implantação das consultas já selecionadas para essa sessão. A lista nesta página diferencia-se da página anterior pela alteração da coluna **Pode implantar** para **Pode reverter**. Essa coluna pode ser *True* ou *False* dependendo se a otimização de consulta implantada pode ser revertida e seu guia de plano e removido.

    ![Etapa 5 do QTA](../../relational-databases/performance/media/qta-step5.png "Etapa 5 do QTA")

    Se em um momento posterior houver a necessidade de reverter para uma otimização proposta, selecione a consulta relevante e clique em **Reverter**. Esse guia de plano de consulta será removido e a lista será atualizada para remover a consulta revertida. Observe na imagem abaixo que a consulta 8 foi removida.

    ![Etapa 5 do QTA – reversão](../../relational-databases/performance/media/qta-step5-rollback.png "Etapa 5 do QTA – reversão") 

    > [!NOTE]
    > A exclusão de uma sessão fechada **não** exclui nenhum guia de plano já implantado.   
    > Ao excluir uma sessão que implantou guias de plano, você não poderá usar o QTA para reversão.    
    > Nesse caso, pesquise guias de plano usando a tabela de sistema [sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) e exclua manualmente usando [sp_control_plan_guide](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
Requer a associação à função **db_owner**.
  
## <a name="see-also"></a>Consulte Também  
 [Níveis de compatibilidade e atualizações do Mecanismo de Banco de Dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)    
 [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [Alterar o modo de compatibilidade do banco de dados e usar o Repositório de Consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)       
 [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Dicas de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint)     
 [Estimador de Cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md)     
 [Ajuste automático](../../relational-databases/automatic-tuning/automatic-tuning.md)      
