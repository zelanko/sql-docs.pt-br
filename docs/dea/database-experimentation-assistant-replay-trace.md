---
title: Repetir um rastreamento com o Assistente de experimentação do banco de dados para atualizações do SQL Server
description: Repetir um rastreamento com o Assistente de experimentação do banco de dados
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
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 09c3ffe6897107d2b3db0f53b0fdc895ee437efd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273975"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Repetir um rastreamento no Assistente de experimentação do banco de dados

No banco de dados experimentação Assistant (DEA), você pode reproduzir um arquivo de rastreamento capturado em um ambiente de teste atualizado. Por exemplo, considere uma carga de trabalho de produção que é executado no SQL Server 2008 R2. O arquivo de rastreamento para a carga de trabalho deve ser repetido duas vezes: uma vez em um ambiente com a mesma versão do SQL Server que é executado em produção e novamente um ambiente que tem a versão de destino de atualização do SQL Server, como o SQL Server 2016.

> [!NOTE]
> Para executar esta ação, você deve configurar manualmente as máquinas virtuais ou computadores físicos a execução de rastreamentos do Distributed Replay. Para obter mais informações, consulte [instalação de controlador e os clientes do Distributed Replay](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/).
>
>

## <a name="create-a-trace-replay"></a>Criar uma reprodução de rastreamento

No DEA, selecione o ícone de menu. No menu expandido, selecione **reproduzir rastreamentos** ao lado do ícone play.

![Selecione reproduzir rastreamentos no menu](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> O computador do controlador Distributed Replay requer permissões à conta de usuário que você usa para o remoto.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Conceder acesso ao controlador do Distributed Replay

1. No prompt de comando, digite **dcomcnfg** para abrir o **serviços de componentes** interface.
1. Expandir **serviços de componentes** > **computadores** > **meu computador** > **DCOM Config**  >  **DReplayController**.
1. Clique com botão direito **DReplayController**e, em seguida, selecione **propriedades**.
1. Sobre o **segurança** guia, selecione **editar** para adicionar a conta de usuário.
1. Selecione **OK**.

### <a name="verify-setup"></a>Verifique se o programa de instalação

1.  **Caminho de instalação do SQL Server**: Insira o caminho para onde o SQL Server está instalado. Por exemplo, c:\\arquivos de programas (x86)\\Microsoft SQL Server\\120.
1.  **O nome de computador do controlador**: Insira um nome para a máquina que foi configurado como o controlador. Este computador está executando o serviço do Windows chamado SQL Server Distributed Replay controller. Controlador do Distributed Replay orquestra as ações dos clientes do Distributed Replay. Cada ambiente de Distributed Replay pode conter apenas uma instância de controlador.
1.  **Nomes de computador cliente**: Insira um nome para cada computador cliente, separado por vírgulas. Exemplo: client1, client2. Você pode ter até cinco controladores de cliente. Os clientes são um ou mais máquinas, físicas ou virtuais, que executam o serviço Windows denominado cliente do SQL Server Distributed Replay. Os clientes do Distributed Replay trabalham juntos para simular cargas de trabalho em uma instância do SQL Server. Pode haver um ou mais clientes em cada ambiente do Distributed Replay.
1.  Selecione **Avançar**.

### <a name="select-a-trace"></a>Selecione um rastreamento

1.  **Caminho do arquivo de rastreamento**: Insira o caminho para o arquivo de rastreamento de entrada (. TRC).
1.  **Caminho para armazenar a reprodução de pré-processamento saída**:  
    \- Se você ainda não tiver o arquivo IRF, digite o caminho para o local onde você deseja armazenar o arquivo IRF e saídas de outros pré-processamento.  
    \- Se você já tiver o arquivo IRF, digite o caminho para os arquivos IRF.
1. Selecione **Avançar**.

### <a name="replay-a-trace"></a>Repetir um rastreamento

1.  **Nome do arquivo de rastreamento**: Insira um nome de arquivo de rastreamento.
1.  **Tamanho máximo do arquivo (MB)**: Insira um valor de tamanho de substituição de arquivo de rastreamento. O padrão é de 200 MB. Você pode inserir um valor personalizado.
1.  **Caminho para armazenar a saída de rastreamento de reprodução**: Insira o caminho do arquivo de saída. TRC.
1.  **Nome da instância do SQL Server**:  Insira o nome da instância do SQL Server na qual reproduzir rastreamentos.
1.  Selecione **iniciar**.

Se as informações inseridas for válidas, o processo de Distributed Replay é iniciado. Caso contrário, os boses de texto que têm informações incorretas são realçadas com vermelho. Certifique-se de que os valores inseridos estão corretos e, em seguida, selecione **iniciar**.

Aguarde até que a reprodução é concluída em execução para ver o local que você especificou. Selecione o ícone de sino na parte inferior do menu à esquerda para monitorar o progresso de reprodução.

![Progresso de rastreamentos de reprodução](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>Perguntas frequentes sobre a reprodução de rastreamento

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>Quais permissões de segurança necessário iniciar uma captura de reprodução no meu servidor de destino?

- O usuário do Windows que está executando a operação de rastreamento no aplicativo DEA deve ter direitos sysadmin no computador de destino executando o SQL Server. Esses direitos de usuário são necessários para iniciar um rastreamento.
- A conta de serviço sob a qual o computador de destino executando o SQL Server está executando deve ter acesso de gravação ao caminho do arquivo de rastreamento especificado.
- A conta de serviço sob a qual os serviços Distributed Replay Client estão executando deve ter direitos de usuário para se conectar ao computador de destino executando o SQL Server e executar consultas.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>Pode iniciar mais de uma reprodução na mesma sessão?

Sim, você pode iniciar várias repetições e acompanhá-las até a conclusão na mesma sessão.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>Pode iniciar mais de uma reprodução em paralelo?

Sim, mas não com o mesmo conjunto de máquinas selecionadas no **controlador mais clientes**. O controlador e os clientes será ocupados. Configurar um conjunto separado de máquinas sob **controlador mais cliente** para iniciar uma reprodução em paralela.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>Quanto tempo uma reprodução normalmente demora para concluir?

Uma reprodução geralmente leva a mesma quantidade de tempo em que o rastreamento de origem mais a quantidade de tempo que leva para pré-processar o rastreamento de origem. No entanto, se os computadores cliente que estão registrados com o controlador não são suficientes para gerenciar a carga que é produzida a partir da reprodução, a reprodução pode levar mais tempo para concluir. Você pode registrar até 16 máquinas de cliente com o controlador.

### <a name="how-large-do-target-trace-files-get"></a>Quão grande obtenho os arquivos de rastreamento de destino?

O rastreamento de destino arquivos que podem ser entre 5 e 15 vezes o tamanho do rastreamento de origem. O tamanho do arquivo se baseia na quantidade de consultas é executadas. Por exemplo, blobs de plano de consulta podem ser grandes. Se as estatísticas para essas consultas são alterados com frequência, mais eventos são capturados.

### <a name="why-do-i-need-to-restore-databases"></a>Por que eu preciso restaurar bancos de dados?

SQL Server é um sistema de gerenciamento de banco de dados relacional com monitoração de estado. Para executar corretamente um A / de teste de B, o estado do banco de dados deve ser mantida em todos os momentos. Caso contrário, você poderá ver erros nas consultas durante a reprodução não aparecerá na produção. Para evitar esses erros, recomendamos que você faça um backup antes da captura da origem. Da mesma forma, a restauração do backup no computador de destino executando o SQL Server é necessário para evitar erros durante a reprodução.

### <a name="what-does-pass--on-the-replay-page-mean"></a>O que é "aprovado %" em que a média da página de reprodução?

**Passar %** significa que apenas uma porcentagem das consultas passada. Você pode diagnosticar se o número de erros é esperado. Os erros podem ser esperados ou os erros podem ocorrer porque o banco de dados perdeu sua integridade. Se o valor para **pass %** não é o esperado, você pode parar o rastreamento e examinar o arquivo de rastreamento no SQL Profiler para ver quais consultas não obteve êxito.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>Como posso examinar os eventos de rastreamento que foram coletados durante a reprodução?

Abra um arquivo de rastreamento de destino e exibi-lo no SQL Profiler. Ou, se você quiser fazer modificações para a captura de reprodução, todos os scripts do SQL Server estão disponíveis em c:\\arquivos de programas (x86)\\Microsoft Corporation\\Assistente de experimentação do banco de dados\\Scripts\\ StartReplayCapture.sql.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>Quais eventos de rastreamento DEA coletar durante a reprodução?

DEA captura eventos de rastreamento que contêm informações relacionadas ao desempenho. A configuração de captura é no script StartReplayCaptureTrace.sql. Esses eventos são eventos de rastreamento do SQL Server típicos que estão listados na [sp_trace_setevent (Transact-SQL) documentação de referência](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Solucionar problemas de reprodução de rastreamento

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>Não é possível conectar-se ao computador que está executando o SQL Server

- Confirme se o nome do computador executando o SQL Server é válido. Para confirmar, tente se conectar ao servidor usando o SQL Server Management Studio (SSMS).
- Confirme que a configuração do firewall não bloqueie conexões com o computador executando o SQL Server.
- Confirme se o usuário tem os direitos de usuário necessário.
- Confirme se a conta de serviço do cliente Distributed Replay tem acesso ao computador que executa o SQL Server.

Você pode obter mais detalhes nos logs em % temp %\\DEA. Se o problema persistir, entre em contato com a equipe de produto.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>Não é possível conectar-se ao controlador do Distributed Replay

- Verifique se que o serviço Distributed Replay controller está em execução no computador do controlador. Para verificar, use as ferramentas de gerenciamento de reprodução distribuída (execute o comando `dreplay.exe status -f 1`).
- Se a reprodução é iniciada remotamente:
  - Confirme que o computador que executa DEA pode fazer um ping bem-sucedido o controlador. Confirme que as configurações de firewall permitem conexões de acordo com as instruções de **configurar o ambiente de reprodução** página. Para obter mais informações, consulte o artigo [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Certifique-se de que o DCOM de inicialização remota e ativação remota são permitidas para o usuário do controlador do Distributed Replay.
  - Certifique-se de que os direitos de usuário de acesso remoto do DCOM são permitidos para o usuário do Distributed Replay controller.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>O caminho do arquivo de rastreamento existe em Meu computador. Por que Distributed Replay controller não é possível encontrá-lo?

Distributed Replay pode acessar somente os recursos de disco local. Você deve copiar arquivos de origem de rastreamento para a máquina do controlador Distributed Replay antes de iniciar a reprodução. Além disso, você deve fornecer o caminho no DEA **Replay novo** página. 

Caminhos UNC não são compatíveis com o Distributed Replay. Caminhos de reprodução distribuídos devem ser caminhos absolutos de locais para o primeiro arquivo de rastreamento de origem, incluindo a extensão.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>Por que não é possível navegar para arquivos na página de reprodução de novo?

Porque nós não é possível procurar pastas de um computador remoto, procurando arquivos não é útil. Copiando e colando os caminhos absolutos são mais eficiente.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>Comecei a reprodução com um rastreamento, mas o Distributed Replay não repetir todos os eventos

Esse problema pode ocorrer porque o arquivo de rastreamento não tem eventos reproduzíveis ou não ter informações sobre como reproduzir eventos. Confirme se o caminho do arquivo de rastreamento fornecido é um arquivo de rastreamento de origem. O arquivo de origem de rastreamento é criado usando a configuração fornecida no script StartCaptureTrace.sql.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>Eu vejo "Ocorreu um erro inesperado!" Quando tento pré-processar Meus arquivos de rastreamento usando o controlador do Distributed Replay do SQL Server 2017

Esse problema é conhecido na versão RTM do SQL Server 2017. Para obter mais informações, consulte [um erro inesperado ao usar o recurso de DReplay para repetir um rastreamento capturado no SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
O problema foi resolvido no 1 atualização cumulativa mais recente do SQL Server 2017. Baixe a versão mais recente do [atualização cumulativa 1 para SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="next-steps"></a>Próximas etapas

- Para criar um relatório de análise que ajuda você a obter informações sobre as alterações propostas, consulte [crie relatórios](database-experimentation-assistant-create-report.md).

- Para obter uma introdução 19 minutos DEA e demonstração, assista ao vídeo a seguir:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
