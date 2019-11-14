---
title: Reproduzir um rastreamento para atualizações de SQL Server
description: Reproduzir um rastreamento com Assistente para Experimentos de Banco de Dados para atualizações de SQL Server
ms.custom: seo-lt-2019
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
ms.openlocfilehash: b1607aefdc8495f374b2586b0b896f20e87f62d1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056706"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Reproduzir um rastreamento no Assistente para Experimentos de Banco de Dados

No Assistente para Experimentos de Banco de Dados (DEA), você pode reproduzir um arquivo de rastreamento capturado em um ambiente de teste atualizado. Por exemplo, considere uma carga de trabalho de produção que é executada no SQL Server 2008 R2. O arquivo de rastreamento para a carga de trabalho deve ser repetido duas vezes: uma vez em um ambiente com a mesma versão do SQL Server que é executado na produção e novamente em um ambiente que tem a versão de SQL Server de destino de atualização, como SQL Server 2016.

> [!NOTE]
> Para executar essa ação, você deve configurar manualmente máquinas virtuais ou máquinas físicas para executar rastreamentos de Distributed Replay. Para obter mais informações, consulte [Distributed Replay instalação do controlador e dos clientes](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
>
>

## <a name="create-a-trace-replay"></a>Criar uma reprodução de rastreamento

Em DEA, selecione o ícone de menu. No menu expandido, selecione **reproduzir rastreamentos** ao lado do ícone reproduzir.

![Selecione reproduzir rastreamentos no menu](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> O computador do controlador de Distributed Replay requer permissões para a conta de usuário que você usa para o remoto.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Conceder acesso ao controlador de Distributed Replay

1. Em um prompt de comando, insira **DCOMCNFG** para abrir a interface de **serviços de componentes** .
1. Expanda **serviços de componentes** > **computadores** > **meu computador** > **Configuração DCOM** > **DReplayController**.
1. Clique com o botão direito do mouse em **DReplayController**e selecione **Propriedades**.
1. Na guia **segurança** , selecione **Editar** para adicionar a conta de usuário.
1. Selecione **OK**.

### <a name="verify-setup"></a>Verificar configuração

1.  **Caminho de instalação do SQL Server**: Insira o caminho para onde o SQL Server está instalado. Por exemplo, C:\\arquivos de programas (x86)\\Microsoft SQL Server\\120.
1.  **Nome do computador do controlador**: Insira um nome para o computador que foi configurado como o controlador. Este computador está executando o serviço do Windows chamado SQL Server controlador de Distributed Replay. O controlador de Distributed Replay orquestra as ações dos clientes Distributed Replay. Cada ambiente de Distributed Replay pode conter apenas uma instância de controlador.
1.  **Nomes de computador cliente**: Insira um nome para cada computador cliente, separados por vírgulas. Exemplo: CLIENT1, CLIENT2. Você pode ter até cinco controladores de cliente. Os clientes são um ou mais computadores, físicos ou virtuais, que executam o serviço do Windows chamado SQL Server Distributed Replay Client. Os clientes do Distributed Replay trabalham juntos para simular cargas de trabalho em uma instância do SQL Server. Pode haver um ou mais clientes em cada ambiente do Distributed Replay.
1.  Selecione **Avançar**.

### <a name="select-a-trace"></a>Selecionar um rastreamento

1.  **Caminho para o arquivo de rastreamento**: Insira o caminho para o arquivo de rastreamento de entrada (. trc).
1.  **Caminho para armazenar saída de pré-processamento de reprodução**:  
    \- se você ainda não tiver o arquivo IRF, insira o caminho para o local onde você deseja armazenar o arquivo IRF e outras saídas de pré-processamento.  
    \- se você já tiver o arquivo IRF, insira o caminho para os arquivos IRF.
1. Selecione **Avançar**.

### <a name="replay-a-trace"></a>Reproduzir um rastreamento

1.  **Nome do arquivo de rastreamento**: Insira um nome de arquivo de rastreamento.
1.  **Tamanho máximo do arquivo (MB)** : Insira um valor de tamanho de substituição do arquivo de rastreamento. O padrão é 200 MB. Você pode inserir um valor personalizado.
1.  **Caminho para armazenar a saída do rastreamento de reprodução**: Insira o caminho para o arquivo output. trc.
1.  **Nome da instância do SQL Server**: Insira o nome da instância de SQL Server na qual os rastreamentos são reproduzidos.
1.  Selecione **Iniciar**.

Se as informações inseridas forem válidas, o processo de Distributed Replay será iniciado. Caso contrário, o texto Boses com informações incorretas será realçado com vermelho. Verifique se os valores inseridos estão corretos e, em seguida, selecione **Iniciar**.

Aguarde até que a reprodução seja concluída em execução para ver o local que você especificou. Selecione o ícone de sino na parte inferior do menu à esquerda para monitorar o progresso da reprodução.

![Progresso da reprodução de rastreamentos](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>Perguntas frequentes sobre a reprodução de rastreamento

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>Quais permissões de segurança preciso para iniciar uma captura de reprodução no meu servidor de destino?

- O usuário do Windows que está executando a operação de rastreamento no aplicativo DEA deve ter direitos sysadmin no computador de destino que executa o SQL Server. Esses direitos de usuário são necessários para iniciar um rastreamento.
- A conta de serviço sob a qual o computador de destino que executa o SQL Server está em execução deve ter acesso de gravação ao caminho do arquivo de rastreamento especificado.
- A conta de serviço sob a qual os serviços de cliente do Distributed Replay estão em execução deve ter direitos de usuário para se conectar ao computador de destino que executa o SQL Server e executar consultas.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>Posso iniciar mais de uma reprodução na mesma sessão?

Sim, você pode iniciar várias repetições e rastreá-las para conclusão na mesma sessão.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>Posso iniciar mais de uma reprodução em paralelo?

Sim, mas não com o mesmo conjunto de computadores selecionado no **controlador mais clientes**. O controlador e os clientes estarão ocupados. Configure um conjunto separado de computadores no **controlador mais o cliente** para iniciar uma reprodução paralela.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>Quanto tempo uma reprodução costuma demorar para ser concluída?

Uma reprodução normalmente leva o mesmo período de tempo que o rastreamento de origem, além da quantidade de tempo que leva para pré-processar o rastreamento de origem. No entanto, se os computadores cliente registrados com o controlador não forem suficientes para gerenciar a carga produzida da reprodução, a reprodução poderá levar mais tempo para ser concluída. Você pode registrar até 16 computadores cliente com o controlador.

### <a name="how-large-do-target-trace-files-get"></a>Quanto tamanho os arquivos de rastreamento de destino são obtidos?

Os arquivos de rastreamento de destino podem estar entre 5 e 15 vezes o tamanho do rastreamento de origem. O tamanho do arquivo é baseado em quantas consultas são executadas. Por exemplo, os blobs de plano de consulta podem ser grandes. Se as estatísticas dessas consultas forem alteradas com frequência, mais eventos serão capturados.

### <a name="why-do-i-need-to-restore-databases"></a>Por que preciso restaurar bancos de dados?

SQL Server é um sistema de gerenciamento de banco de dados relacional com estado. Para executar corretamente um teste A/B, o estado do banco de dados deve ser mantido sempre. Caso contrário, você poderá ver erros em consultas durante a repetição que não aparecerão na produção. Para evitar esses erros, recomendamos que você faça um backup logo antes da captura de origem. Da mesma forma, é necessário restaurar o backup no computador de destino que executa o SQL Server para evitar erros durante a repetição.

### <a name="what-does-pass--on-the-replay-page-mean"></a>O que significa "Pass%" na página de reprodução?

A **passagem%** significa que apenas uma porcentagem de consultas foi aprovada. Você pode diagnosticar se o número de erros é esperado. Os erros podem ser esperados ou os erros podem ocorrer porque o banco de dados perdeu sua integridade. Se o valor da **passagem%** não for o esperado, você poderá interromper o rastreamento e examinar o arquivo de rastreamento no SQL Profiler para ver quais consultas não foram bem sucedidos.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>Como posso examinar os eventos de rastreamento que foram coletados durante a reprodução?

Abra um arquivo de rastreamento de destino e exiba-o no SQL Profiler. Ou, se você quiser fazer modificações na captura de reprodução, todos os scripts de SQL Server estarão disponíveis em C:\\arquivos de programas (x86)\\Microsoft Corporation\\Assistente para Experimentos de Banco de Dados\\scripts\\StartReplayCapture. Sql.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>Quais eventos de rastreamento o DEA coleta durante a reprodução?

O DEA captura eventos de rastreamento que contêm informações relacionadas ao desempenho. A configuração de captura está no script StartReplayCaptureTrace. Sql. Esses eventos são típicos SQL Server eventos de rastreamento listados na [documentação de referência do sp_trace_setevent (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Solucionar problemas de reprodução de rastreamento

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>Não consigo me conectar ao computador que está executando o SQL Server

- Confirme se o nome do computador que executa o SQL Server é válido. Para confirmar, tente se conectar ao servidor usando SQL Server Management Studio (SSMS).
- Confirme se a configuração do firewall não bloqueia conexões com o computador que executa o SQL Server.
- Confirme se o usuário tem os direitos de usuário necessários.
- Confirme se a conta de serviço do cliente Distributed Replay tem acesso ao computador que está executando o SQL Server.

Você pode obter mais detalhes nos logs em% temp%\\DEA. Se o problema persistir, entre em contato com a equipe do produto.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>Não consigo me conectar ao controlador de Distributed Replay

- Verifique se o serviço do controlador de Distributed Replay está em execução no computador do controlador. Para verificar, use as ferramentas de gerenciamento de Distributed Replay (execute o comando `dreplay.exe status -f 1`).
- Se a reprodução for iniciada remotamente:
  - Confirme se o computador que executa o DEA pode executar ping no controlador com êxito. Confirme se as configurações de firewall permitem conexões de acordo com as instruções na página **Configurar ambiente de reprodução** . Para obter mais informações, consulte o artigo [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Verifique se o início remoto DCOM e a ativação remota são permitidos para o usuário do controlador de Distributed Replay.
  - Verifique se os direitos de usuário de acesso remoto DCOM são permitidos para o usuário do controlador de Distributed Replay.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>O caminho do arquivo de rastreamento existe em meu computador. Por que o controlador não pode Distributed Replay encontrá-lo?

Distributed Replay pode acessar apenas os recursos de disco local. Você deve copiar os arquivos de rastreamento de origem para o computador do controlador de Distributed Replay antes de iniciar a reprodução. Além disso, você deve fornecer o caminho na página **nova reprodução** do DEA. 

Os caminhos UNC não são compatíveis com Distributed Replay. Caminhos de Distributed Replay devem ser caminhos locais e absolutos para o primeiro arquivo de rastreamento de origem, incluindo a extensão.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>Por que não consigo procurar arquivos na nova página de reprodução?

Como não podemos navegar nas pastas de um computador remoto, procurar arquivos não é útil. Copiar e colar os caminhos absolutos é mais eficiente.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>Comecei a repetir com um rastreamento, mas Distributed Replay não reproduziu nenhum evento

Esse problema pode ocorrer porque o arquivo de rastreamento não tem eventos que podem ser reproduzidos ou não tem informações sobre como repetir eventos. Confirme se o caminho do arquivo de rastreamento fornecido é um arquivo de rastreamento de origem. O arquivo de rastreamento de origem é criado usando a configuração fornecida no script StartCaptureTrace. Sql.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>Eu vejo "ocorreu um erro inesperado!" Quando tento pré-processar meus arquivos de rastreamento usando o controlador de Distributed Replay SQL Server 2017

Esse problema é conhecido na versão RTM do SQL Server 2017. Para obter mais informações, consulte [erro inesperado ao usar o recurso DReplay para reproduzir um rastreamento capturado no SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
O problema foi resolvido na atualização cumulativa 1 mais recente para o SQL Server 2017. Baixe a versão mais recente da [atualização cumulativa 1 para SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="next-steps"></a>Próximas etapas

- Para criar um relatório de análise que ajuda você a obter informações sobre as alterações propostas, consulte [criar relatórios](database-experimentation-assistant-create-report.md).

- Para uma introdução de 19 minutos ao DEA e à demonstração, Assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
