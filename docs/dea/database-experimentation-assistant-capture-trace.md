---
title: Capturar um rastreamento no Assistente para Experimentos de Banco de Dados para atualizações de SQL Server
description: Capturar um rastreamento no Assistente para Experimentos de Banco de Dados
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: 3887daff7807d57244449d4f35d220bb47b8f10d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653816"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Capturar um rastreamento no Assistente para Experimentos de Banco de Dados

Você pode usar uma captura de rastreamento no Assistente para Experimentos de Banco de Dados (DEA) para criar um arquivo de rastreamento que tenha um log de eventos de servidor capturados. Um evento de servidor capturado é um evento que ocorre em um servidor específico durante um período de tempo específico. Uma captura de rastreamento deve ser executada uma vez por servidor.

Antes de iniciar uma captura de rastreamento, certifique-se de fazer backup de todos os bancos de dados de destino.

O cache de consulta no SQL Server pode afetar os resultados da avaliação. Recomendamos que você reinicie o serviço de SQL Server (MSSQLSERVER) no aplicativo de serviços para melhorar a consistência dos resultados da avaliação.

## <a name="create-a-trace-capture"></a>Criar uma captura de rastreamento

1. No DEA, selecione o ícone de menu no menu à esquerda. No menu expandido, selecione **rastreamentos de captura** ao lado do ícone da câmera.

    ![Selecionar rastreamentos de captura no menu](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. Em **nova captura**, insira ou selecione as seguintes informações:

    - **Nome da instância do SQL Server**: Insira um nome para o computador executando SQL Server no qual você deseja capturar um rastreamento de servidor.
    - **Nome do banco de dados**: Insira um nome para um banco de dados no qual iniciar um rastreamento de banco de dados. Se você não especificar um banco de dados, o rastreamento será capturado em todos os bancos no servidor.
    - **Nome do arquivo de rastreamento**: Insira um nome para o arquivo de rastreamento para a captura.
    - **Tamanho máximo do arquivo (MB)** : Selecione o tamanho da sobreposição dos arquivos. Um novo arquivo é criado conforme necessário no tamanho do arquivo selecionado. O tamanho de substituição recomendado é 200 MB.
    - **Duração (em min)** : Selecione o período de tempo (em minutos) que você deseja que a captura de rastreamento seja executada.
    - **Caminho para armazenar o arquivo de rastreamento de saída**: Selecione o caminho de destino para o arquivo de rastreamento. 

    > [!NOTE]
    > O caminho do arquivo para o arquivo de rastreamento deve estar no computador que está executando o SQL Server. Se o serviço de SQL Server não estiver definido para uma conta específica, o serviço poderá precisar de permissões de gravação para a pasta especificada para que o arquivo de rastreamento seja gravado.
    >
    >

    ![Nova página de captura](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>Iniciar a captura de rastreamento

Depois de inserir ou selecionar as informações necessárias, selecione **Iniciar** para iniciar a captura de rastreamentos. Se as informações inseridas forem válidas, o processo de captura de rastreamento será iniciado. Caso contrário, as caixas de texto com entradas inválidas serão realçadas com vermelho. 

Verifique se os valores selecionados ou inseridos estão corretos e, em seguida, selecione **Iniciar**.

Quando a captura de rastreamento for concluída, localize o novo arquivo de rastreamento no local do arquivo que você especificou no **caminho para armazenar o arquivo de rastreamento de saída**. Selecione o ícone de sino na parte inferior do menu à esquerda para monitorar o progresso da captura.

![Progresso dos rastreamentos de captura](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>Arquivo de rastreamento

A captura de rastreamento grava um arquivo. trc no local especificado. O arquivo de rastreamento inclui resultados de rastreamento da atividade de um banco de dados SQL Server. Os arquivos TRC são projetados para fornecer mais informações sobre erros detectados e relatados pelo SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Perguntas frequentes sobre a captura de rastreamento

A seguir, algumas perguntas frequentes sobre a captura de rastreamento no DEA.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>Quais eventos são capturados quando executo uma captura de rastreamento em um banco de dados de produção?

A tabela a seguir fornece a lista de eventos e os dados de coluna correspondentes que coletamos para rastreamentos:
  
|Nome do evento|Dados de texto (1)|Dados binários (2)|ID do banco de dados (3)|Nome do host (8)|Nome do aplicativo (10)|Nome de logon (11)|SPID (12)|Hora de início (14)|Hora de término (15)|Nome do banco de dados (35)|Sequência de eventos (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: concluído (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: Iniciando (11)**||*|*|*|*|*|*|*||*|*|*|  
|**Parâmetro de saída RPC (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL: BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Logon de auditoria (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Logout de auditoria (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Preparar SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**SQL preparado para exec (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>Há um efeito de desempenho no meu servidor de produção quando a captura de rastreamento está em execução?
    
Sim, há um mínimo de efeito de desempenho durante a coleta de rastreamento. Em nossos testes, encontramos cerca de 3% de pressão de memória.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>Que tipo de permissões são necessárias para capturar rastreamentos em uma carga de trabalho de produção?
    
- O usuário do Windows que executa a operação de rastreamento no aplicativo DEA deve ter direitos sysadmin no computador que está executando o SQL Server.
- A conta de serviço usada no computador que executa o SQL Server deve ter acesso de gravação ao caminho do arquivo de rastreamento especificado.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>Posso capturar rastreamentos para todo o servidor ou apenas em um único banco de dados?
    
Você pode usar o DEA para capturar rastreamentos para todos os bancos de dados no servidor ou para um único banco.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>Tenho um servidor vinculado configurado em meu ambiente de produção. Essas consultas aparecem nos rastreamentos?
    
Se você estiver executando uma captura de rastreamento para todo o servidor, o rastreamento capturará todas as consultas, incluindo as consultas de servidor vinculado. Para executar uma captura de rastreamento para todo o servidor, deixe a caixa **nome do banco de dados** em **nova captura** vazia.
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>Qual é o tempo mínimo recomendado para rastreamentos de carga de trabalho de produção?
    
Recomendamos que você escolha um horário que melhor represente todo o tempo de sua carga de trabalho. Dessa forma, a análise é executada em todas as consultas em sua carga de trabalho.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>Qual é a importância de fazer um backup de banco de dados logo antes de iniciar uma captura de rastreamento?
    
Antes de iniciar uma captura de rastreamento, certifique-se de fazer backup de todos os seus bancos de dados de destino. O rastreamento capturado no destino 1 e no destino 2 é repetido. Se o estado do banco de dados não for o mesmo, os resultados da experimentação serão distorcidos.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>Posso coletar XEvents em vez de rastreamentos e posso reproduzir o XEvents?
    
Sim. DEA dá suporte a XEvents. Baixe a versão mais recente do DEA e experimente.

## <a name="troubleshoot-trace-captures"></a>Solucionar problemas de capturas de rastreamento

Se você vir um erro ao executar uma captura de rastreamento, examine os seguintes pré-requisitos:

- Confirme se o nome do computador que executa o SQL Server é válido. Para confirmar, tente se conectar ao computador que executa o SQL Server usando o SQL Server Management Studio (SSMS).
- Confirme se a configuração do firewall não bloqueia conexões com o computador que executa o SQL Server.
- Confirme se o usuário tem as permissões listadas nas [perguntas frequentes sobre reprodução](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)de postagem de blog.
- Confirme se o nome do rastreamento não segue a Convenção de substituição padrão\_(captura 1). Em vez disso, tente rastrear nomes\_como captura 1a ou Capture1.

A seguir estão alguns erros possíveis que você pode ver e soluções para solucioná-los:

|Possíveis erros|Solução|  
|---|---|  
|Não é possível iniciar o rastreamento no SQL Server de destino, verifique se você tem as permissões necessárias e se a conta de SQL Server tem acesso de gravação ao código de erro SQL do caminho do arquivo de rastreamento especificado (53)|O usuário que executa a ferramenta DEA deve ter acesso ao computador que executa o SQL Server. O usuário deve ser atribuído à função sysadmin.|  
|Não é possível iniciar o rastreamento no SQL Server de destino, verifique se você tem as permissões necessárias e se a conta de SQL Server tem acesso de gravação ao código de erro SQL do caminho do arquivo de rastreamento especificado (19062)|O caminho de rastreamento especificado pode não existir ou a pasta não tem permissões de gravação para a conta sob a qual os serviços de SQL Server estão em execução (por exemplo, serviço de rede). O caminho deve existir e deve ter as permissões necessárias para que o rastreamento seja iniciado.|  
|Um rastreamento DEA está sendo executado no servidor de destino.|Um rastreamento ativo já está em execução no servidor de destino. Você não pode iniciar um novo rastreamento quando um rastreamento de todo o servidor já está em execução.|  
|Não é possível abrir o banco de dados solicitado para capturar o rastreamento. Esse erro pode ser causado por um nome de banco de dados incorreto.|O banco de dados especificado não existe ou não está acessível para o usuário atual. Use o nome de banco de dados correto.|  

Se você vir quaisquer outros erros rotulados como *código de erro SQL*, consulte [mecanismo de banco de dados erros](https://docs.microsoft.com/sql/relational-databases/errors-events/database-engine-events-and-errors) para obter descrições detalhadas.

## <a name="next-steps"></a>Próximas etapas

- Para saber como configurar as ferramentas de Distributed Replay no SQL Server antes de reproduzir um rastreamento capturado, consulte [Configurar reprodução](database-experimentation-assistant-configure-replay.md).

- Para uma introdução de 19 minutos ao DEA e à demonstração, Assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
