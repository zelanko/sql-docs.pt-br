---
title: Capturar um rastreamento no Assistente de experimentação do banco de dados para atualizações do SQL Server
description: Capturar um rastreamento no Assistente de experimentação do banco de dados
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
ms.openlocfilehash: ab361c4e83ae5e2b2bb6614bdc4a513e0bdd77ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058999"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Capturar um rastreamento no Assistente de experimentação do banco de dados

Você pode usar uma captura de rastreamento no banco de dados experimentação Assistant (DEA) para criar um arquivo de rastreamento que tem um log de eventos de servidor capturados. Um evento capturado no servidor é um evento que ocorre em um servidor específico durante um período de tempo específico. Uma captura de rastreamento deve ser executada uma vez por servidor.

Antes de iniciar uma captura de rastreamento, certifique-se de que você faça backup de todos os bancos de dados de destino.

Cache de consulta no SQL Server pode afetar os resultados da avaliação. É recomendável que você reinicie o serviço do SQL Server (MSSQLSERVER) no aplicativo de serviços para melhorar a consistência dos resultados da avaliação.

## <a name="create-a-trace-capture"></a>Criar uma captura de rastreamento

1. No DEA, selecione o ícone de menu no menu à esquerda. No menu expandido, selecione **capturar rastreamentos** ao lado do ícone de câmera.

    ![Selecione capturar rastreamentos no menu](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. Sob **nova captura**, insira ou selecione as seguintes informações:

    - **Nome da instância do SQL Server**: Insira um nome para o computador executando o SQL Server no qual você deseja capturar um rastreamento de servidor.
    - **Nome do banco de dados**: Insira um nome para um banco de dados no qual iniciar um rastreamento de banco de dados. Se você não especificar um banco de dados, o rastreamento é capturado em todos os bancos de dados no servidor.
    - **Nome do arquivo de rastreamento**: Insira um nome para o arquivo de rastreamento para a captura.
    - **Tamanho máximo do arquivo (MB)** : Selecione o tamanho de substituição para arquivos. Um novo arquivo é criado, conforme necessário em que o tamanho do arquivo que você selecionar. O tamanho recomendado de substituição é de 200 MB.
    - **Duração (em min)** : Selecione o período de tempo (em minutos) que você deseja que a captura de rastreamento seja executada.
    - **Caminho para armazenar o arquivo de saída de rastreamento**: Selecione o caminho de destino para o arquivo de rastreamento. 

    > [!NOTE]
    > O caminho do arquivo para o arquivo de rastreamento deve ser no computador que executa o SQL Server. Se o serviço SQL Server não está definido para uma conta específica, é possível que o serviço precisa gravar a permissões para a pasta especificada para o arquivo de rastreamento a serem gravados.
    >
    >

    ![Nova página de captura](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>Inicie a captura de rastreamento

Depois que você insira ou selecione as informações necessárias, selecione **iniciar** para iniciar a captura de rastreamentos. Se as informações inseridas for válidas, inicia o processo de captura de rastreamento. Caso contrário, as caixas de texto que possuem entradas inválidas são realçadas com vermelho. 

Certifique-se de que os valores que você selecionou ou inseridas estão corretos e, em seguida, selecione **iniciar**.

Quando a captura de rastreamento é concluída em execução, localize o novo arquivo de rastreamento no local do arquivo que você especificou no **caminho para armazenar o arquivo de saída de rastreamento**. Selecione o ícone de sino na parte inferior do menu à esquerda para monitorar o progresso da captura.

![Capturar o progresso de rastreamentos](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>Arquivo de rastreamento

A captura de rastreamento grava em um arquivo. TRC no local especificado. O arquivo de rastreamento inclui resultados de rastreamento da atividade de um banco de dados do SQL Server. Arquivos TRC foram projetados para fornecer mais informações sobre erros que são detectados e relatado pelo SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Perguntas frequentes sobre a captura de rastreamento

A seguir está algumas perguntas frequentes sobre a captura de rastreamento em DEA.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>Quais eventos são capturados quando eu executo uma captura de rastreamento em um banco de dados de produção?

A tabela a seguir fornece a lista de eventos e os dados da coluna correspondente que coletamos para rastreamentos:
  
|Nome do evento|Dados de texto (1)|Dados binários (2)|ID do banco de dados (3)|Nome do host (8)|Nome do aplicativo (10)|Nome de logon (11)|SPID (12)|Hora de início (14)|Hora de término (15)|Nome do banco de dados (35)|Sequência de eventos (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: concluída (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: iniciando (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC Output Parameter (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL: BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Logon de auditoria (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Auditar logoff (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Prepare SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**EXEC preparada SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>Há um efeito de desempenho do meu servidor de produção quando a captura de rastreamento está em execução?
    
Sim, há um efeito mínimo no desempenho durante a coleta de rastreamento. Em nossos testes, descobrimos sobre uma pressão de memória de % 3.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>Que tipo de permissões são necessárias para capturar rastreamentos em uma carga de trabalho de produção?
    
- O usuário do Windows que executa a operação de rastreamento no aplicativo DEA deve ter direitos sysadmin no computador que executa o SQL Server.
- A conta de serviço usada no computador executando o SQL Server deve ter acesso de gravação ao caminho do arquivo de rastreamento especificado.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>Pode capturar rastreamentos para todo o servidor ou apenas em um único banco de dados?
    
Você pode usar DEA para capturar rastreamentos para todos os bancos de dados no servidor ou para um banco de dados.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>Eu tenho um servidor vinculado configurado no meu ambiente de produção. Essas consultas aparece nos rastreamentos?
    
Se você estiver executando uma captura de rastreamento para todo o servidor, o rastreamento de captura todas as consultas, inclusive as consultas de servidor vinculado. Para executar uma captura de rastreamento para o servidor inteiro, deixe o **nome do banco de dados** caixa sob **nova captura** vazio.
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>O que é o tempo mínimo recomendado para rastreamentos de carga de trabalho de produção?
    
É recomendável que você escolha um horário que melhor representa a totalidade de sua carga de trabalho. Dessa forma, a análise é executada em todas as consultas na carga de trabalho.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>Quão importante é fazer um backup de banco de dados correto antes de começar uma captura de rastreamento?
    
Antes de iniciar uma captura de rastreamento, certifique-se de que você faça backup de todos os seus bancos de dados de destino. O rastreamento capturado no destino 1 e 2 de destino é repetido. Se o estado do banco de dados não é o mesmo, os resultados da experimentação são distorcidos.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>Posso coletar XEvents, em vez de rastreamentos e pode, reproduzir XEvents?
    
Sim. DEA dá suporte a XEvents. Baixe a versão mais recente do DEA e experimentá-lo.

## <a name="troubleshoot-trace-captures"></a>Solucionar problemas de captura de rastreamento

Se você vir um erro ao executar uma captura de rastreamento, consulte os seguintes pré-requisitos:

- Confirme se o nome do computador executando o SQL Server é válido. Para confirmar, tente se conectar ao computador que executa o SQL Server usando o SQL Server Management Studio (SSMS).
- Confirme que a configuração do firewall não bloqueie conexões com o computador executando o SQL Server.
- Confirme se o usuário tem as permissões que são listadas na postagem de blog [perguntas frequentes sobre a reprodução](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/).
- Confirme que o nome do rastreamento não segue a convenção padrão de substituição (capturar\_1). Em vez disso, tente os nomes de rastreamento como captura\_1A ou Capture1.

A seguir estão alguns erros possíveis, que você poderá ver e soluções para resolvê-los:

|Possíveis erros|Solução|  
|---|---|  
|Não é possível iniciar o rastreamento no destino do SQL Server, verifique se você tem as permissões necessárias e se a conta do SQL Server tem acesso de gravação ao caminho do arquivo de rastreamento especificado o código de erro de Sql (53)|O usuário que executa a ferramenta DEA deve ter acesso ao computador que executa o SQL Server. O usuário deve ser atribuído a função sysadmin.|  
|Não é possível iniciar o rastreamento no destino do SQL Server, verifique se você tem as permissões necessárias e se a conta do SQL Server tem acesso de gravação ao caminho do arquivo de rastreamento especificado o código de erro de Sql (19062)|O caminho de rastreamento especificado pode não existir ou a pasta não tem permissões de gravação para a conta sob a qual SQL Server serviços estão em execução (por exemplo, serviço de rede). O caminho deve existir e deve ter as permissões necessárias para iniciar o rastreamento.|  
|Um rastreamento DEA está em execução no momento no servidor de destino.|Um rastreamento ativo já está em execução no servidor de destino. Quando um rastreamento de todo o servidor já está em execução, você não pode iniciar um novo rastreamento.|  
|Não é possível abrir o banco de dados solicitado para capturar o rastreamento. Esse erro pode ser causado por um nome de banco de dados incorreto.|O banco de dados especificado não existe ou não está acessível ao usuário atual. Use o nome do banco de dados correto.|  

Se você ver todos os outros erros rotulados *código de erro de Sql*, consulte [mensagens de erro do sistema](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/cc645603(v=sql.105)) para obter descrições detalhadas e resoluções.
    
## <a name="next-steps"></a>Próximas etapas

- Para saber como configurar as ferramentas do Distributed Replay no SQL Server antes de repetir um rastreamento capturado, consulte [replay configurar](database-experimentation-assistant-configure-replay.md).

- Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
