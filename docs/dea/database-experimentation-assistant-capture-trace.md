---
title: Capturar um rastreamento para atualizações de SQL Server
description: Capturar um rastreamento no Assistente para Experimentos de Banco de Dados para atualizações de SQL Server
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: rajsell
ms.reviewer: mathoma
ms.openlocfilehash: 1c87d791d5a5a16ec3b0d07c6a630f133a7f673c
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289824"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>Capturar um rastreamento no Assistente para Experimentos de Banco de Dados

Você pode usar Assistente para Experimentos de Banco de Dados (DEA) para criar um arquivo de rastreamento com um log de eventos de servidor capturados. Um evento de servidor capturado é um evento que ocorre em um servidor específico durante um período de tempo específico. Uma captura de rastreamento deve ser executada uma vez por servidor.

Antes de iniciar uma captura de rastreamento, certifique-se de fazer backup de todos os bancos de dados de destino.

O cache de consulta no SQL Server pode afetar os resultados da avaliação. Recomendamos que você reinicie o serviço de SQL Server (MSSQLSERVER) no aplicativo de serviços para melhorar a consistência dos resultados da avaliação.

## <a name="configure-a-trace-capture"></a>Configurar uma captura de rastreamento

1. No DEA, na barra de navegação à esquerda, selecione o ícone da câmera e, em seguida, na página **todas as capturas** , selecione **nova captura**.

    ![Criar uma captura no DEA](./media/database-experimentation-assistant-capture-trace/dea-initiate-capture.png)

2. Na página **nova captura** , em **detalhes da captura**, insira ou selecione as seguintes informações:

    - **Nome da captura**: Insira um nome para o arquivo de rastreamento para a captura.
    - **Formato**: especifique o formato (Trace ou XEvents) para a captura.
    - **Duração**: selecione o período de tempo (em minutos) que você deseja que a captura de rastreamento seja executada.
    - **Local de captura**: selecione o caminho de destino para o arquivo de rastreamento.

        > [!NOTE]
        > O caminho do arquivo para o arquivo de rastreamento deve estar no computador que está executando o SQL Server. Se o serviço de SQL Server não estiver definido para uma conta específica, o serviço poderá precisar de permissões de gravação para a pasta especificada para que o arquivo de rastreamento seja gravado.

3. Verifique se você fez um backup selecionando **Sim, fiz o backup manualmente...** .

4. Em **detalhes da captura**, insira ou selecione as seguintes informações:

    - **Tipo de servidor**: especifique o tipo do SQL Server (**SqlServer**, **AzureSqlDb**, **AzureSqlManagedInstance**).
    - **Nome do servidor**: especifique o nome do servidor ou o endereço IP do seu SQL Server.
    - **Tipo de autenticação**: para o tipo de autenticação, selecione **Windows**.
    - **Nome do banco de dados**: Insira um nome para um banco de dados no qual iniciar um rastreamento de banco de dados. Se você não especificar um banco de dados, o rastreamento será capturado em todos os bancos no servidor.

5. Marque ou desmarque as caixas de seleção **criptografar conexão** e **certificado do servidor confiável** , conforme apropriado para seu cenário.

    ![Nova página de captura](./media/database-experimentation-assistant-capture-trace/dea-new-capture.png)

## <a name="start-the-trace-capture"></a>Iniciar a captura de rastreamento

1. Depois de inserir ou selecionar as informações necessárias, selecione **Iniciar** para iniciar a captura de rastreamento.

    Se as informações inseridas forem válidas, o processo de captura de rastreamento será iniciado. Caso contrário, as caixas de texto com entradas inválidas serão realçadas em vermelho. Se você encontrar erros, corrija as entradas necessárias e, em seguida, selecione **Iniciar** novamente.

    Enquanto a captura de rastreamento está em execução, em **detalhes da captura**, o status e o progresso do processo de captura de rastreamento são exibidos.

    ![Monitorar o progresso da captura](./media/database-experimentation-assistant-capture-trace/dea-capture-running.png)

2. Quando a captura de rastreamento for concluída em execução, o novo arquivo de rastreamento (. trc) será salvo no **local de captura** específico durante a configuração inicial.

    ![Captura de rastreamento concluída](./media/database-experimentation-assistant-capture-trace/dea-capture-complete.png)

    O arquivo de rastreamento inclui resultados de rastreamento da atividade de um banco de dados SQL Server. arquivos. trc são projetados para fornecer mais informações sobre erros detectados e relatados pelo SQL Server.

## <a name="frequently-asked-questions-about-trace-capture"></a>Perguntas frequentes sobre a captura de rastreamento

A seguir, algumas perguntas frequentes sobre a captura de rastreamento no DEA.

**P: quais eventos são capturados quando executo uma captura de rastreamento em um banco de dados de produção?**

A tabela a seguir lista os eventos e os dados de coluna correspondentes que o DEA coleta para rastreamentos:
  
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

**P: há um efeito de desempenho no meu servidor de produção quando a captura de rastreamento está em execução?**

Sim, há um mínimo de efeito de desempenho durante a coleta de rastreamento. Em nossos testes, encontramos cerca de 3% de pressão de memória.

**P: que tipo de permissões são necessárias para capturar rastreamentos em uma carga de trabalho de produção?**

- O usuário do Windows que executa a operação de rastreamento no aplicativo DEA deve ter direitos sysadmin no computador que está executando o SQL Server.
- A conta de serviço usada no computador que executa o SQL Server deve ter acesso de gravação ao caminho do arquivo de rastreamento especificado.

**P: posso capturar rastreamentos para todo o servidor ou apenas em um único banco de dados?**

Você pode usar o DEA para capturar rastreamentos para todos os bancos de dados no servidor ou para um único banco.

**P: tenho um servidor vinculado configurado em meu ambiente de produção. Essas consultas aparecem nos rastreamentos?**

Se você estiver executando uma captura de rastreamento para todo o servidor, o rastreamento capturará todas as consultas, incluindo as consultas de servidor vinculado. Para executar uma captura de rastreamento para todo o servidor, deixe a caixa **nome do banco de dados** em **nova captura** vazia.

**P: Qual é o tempo mínimo recomendado para rastreamentos de carga de trabalho de produção?**

Recomendamos que você escolha um horário que melhor represente todo o tempo de sua carga de trabalho. Dessa forma, a análise é executada em todas as consultas em sua carga de trabalho.

**P: Qual é a importância de fazer um backup de banco de dados imediatamente antes de iniciar uma captura de rastreamento?**

Antes de iniciar uma captura de rastreamento, certifique-se de fazer backup de todos os seus bancos de dados de destino. O rastreamento capturado no destino 1 e no destino 2 é repetido. Se o estado do banco de dados não for o mesmo, os resultados da experimentação serão distorcidos.

**P: posso coletar XEvents em vez de rastreamentos e posso reproduzir o XEvents?**

Sim. DEA dá suporte a XEvents. Baixe a versão mais recente do DEA e experimente.

## <a name="troubleshoot-trace-captures"></a>Solucionar problemas de capturas de rastreamento

Se você vir um erro ao executar uma captura de rastreamento, confirme se:

- O nome do computador que executa o SQL Server é válido. Para confirmar, tente se conectar ao computador que executa o SQL Server usando o SQL Server Management Studio (SSMS).
- A configuração do firewall não bloqueia conexões com o computador que executa o SQL Server.
- O usuário tem as permissões listadas nas [perguntas frequentes de reprodução](https://docs.microsoft.com/sql/dea/database-experimentation-assistant-replay-trace?view=sql-server-ver15#frequently-asked-questions-about-trace-replay).
- O nome do rastreamento não segue a Convenção de substituição padrão\_(captura 1). Em vez disso, tente rastrear nomes\_como captura 1a ou Capture1.

A seguir estão alguns erros possíveis que você pode ver e soluções para solucioná-los:

|Possíveis erros|Solução|  
|---|---|  
|Não é possível iniciar o rastreamento no SQL Server de destino, verifique se você tem as permissões necessárias e se a conta de SQL Server tem acesso de gravação ao código de erro SQL do caminho do arquivo de rastreamento especificado (53)|O usuário que executa a ferramenta DEA deve ter acesso ao computador que executa o SQL Server. O usuário deve ser atribuído à função sysadmin.|  
|Não é possível iniciar o rastreamento no SQL Server de destino, verifique se você tem as permissões necessárias e se a conta de SQL Server tem acesso de gravação ao código de erro SQL do caminho do arquivo de rastreamento especificado (19062)|O caminho de rastreamento especificado pode não existir ou a pasta não tem permissões de gravação para a conta sob a qual os serviços de SQL Server estão em execução (por exemplo, serviço de rede). O caminho deve existir e deve ter as permissões necessárias para que o rastreamento seja iniciado.|  
|Um rastreamento DEA está sendo executado no servidor de destino.|Um rastreamento ativo já está em execução no servidor de destino. Você não pode iniciar um novo rastreamento quando um rastreamento de todo o servidor já está em execução.|  
|Não é possível abrir o banco de dados solicitado para capturar o rastreamento. Esse erro pode ser causado por um nome de banco de dados incorreto.|O banco de dados especificado não existe ou não está acessível para o usuário atual. Use o nome de banco de dados correto.|  

Se você vir quaisquer outros erros rotulados como *código de erro SQL*, consulte [mecanismo de banco de dados erros](https://docs.microsoft.com/sql/relational-databases/errors-events/database-engine-events-and-errors) para obter descrições detalhadas.

## <a name="see-also"></a>Confira também

- Para saber como configurar as ferramentas de Distributed Replay no SQL Server antes de reproduzir um rastreamento capturado, consulte [configurar Distributed Replay para assistente para experimentos de banco de dados](database-experimentation-assistant-configure-replay.md).
