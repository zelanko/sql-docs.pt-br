---
title: Reproduzir um rastreamento para atualizações de SQL Server
description: Reproduzir um rastreamento com Assistente para Experimentos de Banco de Dados para atualizações de SQL Server
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
ms.openlocfilehash: 50f082edef5d9a6d4e95b7e37ef6d75f22eb6f2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244846"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>Reproduzir um rastreamento no Assistente para Experimentos de Banco de Dados

No Assistente para Experimentos de Banco de Dados (DEA), você pode reproduzir um arquivo de rastreamento capturado em um ambiente de teste atualizado. Por exemplo, considere uma carga de trabalho de produção que é executada no SQL Server 2008 R2. O arquivo de rastreamento para a carga de trabalho deve ser repetido duas vezes: uma vez em um ambiente com a mesma versão do SQL Server que é executado em produção e uma segunda vez em um ambiente com a versão de destino de atualização SQL Server, como SQL Server 2016.

> [!NOTE]
> Repetir um rastreamento requer que você configure manualmente máquinas virtuais ou computadores físicos para executar Distributed Replay rastreamentos. Para obter mais informações, consulte [configurar Distributed Replay para assistente para experimentos de banco de dados](database-experimentation-assistant-configure-replay.md).
>

## <a name="configure-a-trace-replay-for-target-1"></a>Configurar uma reprodução de rastreamento para o destino 1

Primeiro, você precisa executar uma reprodução de rastreamento no destino 1, que representa o ambiente de produção existente.

1. No DEA, na barra de navegação à esquerda, selecione o ícone de seta e, em seguida, na página **todas as repetições** , selecione **nova reprodução**.

    ![Criar uma reprodução no DEA](./media/database-experimentation-assistant-replay-trace/dea-create-replay.png)

    > [!NOTE]
    > O computador do controlador de Distributed Replay requer permissões para a conta de usuário que você usa para se conectar remotamente.

2. Na página **nova reprodução** , em detalhes da **reprodução**, insira ou selecione as seguintes informações:

    - **Nome de reprodução**: Insira um nome para a reprodução de rastreamento.
    - **Formato de rastreamento de origem**: especifique o formato (Trace ou XEvents) do arquivo de rastreamento de origem.
    - **Caminho completo para o arquivo de origem**: especifique o caminho completo para o arquivo de rastreamento de origem. Se estiver usando o DReplay, o arquivo deverá existir no computador que serve como o controlador DReplay e a conta de usuário exigirá acesso ao arquivo e à pasta.
    - **Ferramenta de reprodução**: Especifique a ferramenta de reprodução (DReplay ou incompilado).
    - **Nome do computador do controlador**: especifique o nome do computador que está servindo como o controlador de Distributed Replay.
    - **Local do rastreamento de reprodução**: especifique o caminho para armazenar arquivos de rastreamento/XEvents associados à reprodução de rastreamento.

        > [!NOTE]
        > Para um banco de dados SQL do Azure ou uma instância gerenciada do banco de dados SQL do Azure, você precisa fornecer o URI de SAS da conta de armazenamento de BLOBs do Azure.

3. Verifique se você restaurou os bancos de dados selecionando a caixa de seleção **Sim, eu restaurei manualmente os bancos de dados** .

4. Em **detalhes da conexão SQL Server**, insira ou selecione as seguintes informações:

    - **Tipo de servidor**: especifique o tipo do SQL Server (**SqlServer**, **AzureSqlDb**, **AzureSqlManagedInstance**).
    - **Nome do servidor**: especifique o nome do servidor ou o endereço IP do seu SQL Server.
    - **Tipo de autenticação**: para o tipo de autenticação, selecione **Windows**.
    - **Nome do banco de dados**: Insira um nome para um banco de dados no qual iniciar um rastreamento do lado do servidor. Se você não especificar um banco de dados, o rastreamento será capturado em todos os bancos no servidor.

5. Marque ou desmarque as caixas de seleção **criptografar conexão** e **certificado do servidor confiável** , conforme apropriado para seu cenário.

    ![Nova página de reprodução](./media/database-experimentation-assistant-replay-trace/dea-new-replay.png)

## <a name="start-the-trace-replay-on-target-1"></a>Iniciar a reprodução de rastreamento no destino 1

- Depois de inserir ou selecionar as informações necessárias, selecione **Iniciar** para iniciar a reprodução de rastreamento.

  Se as informações inseridas forem válidas, o processo de Distributed Replay será iniciado. Caso contrário, as caixas de texto com informações incorretas serão realçadas com vermelho. Verifique se os valores inseridos estão corretos e, em seguida, selecione **Iniciar**.

  ![Reproduzir o progresso no destino 1](./media/database-experimentation-assistant-replay-trace/dea-run-replay-target1.png)

  Você pode monitorar o processo conforme necessário. Quando a execução da reprodução for concluída, o DEA armazenará os resultados em um arquivo no local especificado.

  ![Reproduzir em relação ao destino 1 concluído](./media/database-experimentation-assistant-replay-trace/dea-replay-target1-complete.png)

## <a name="perform-the-trace-replay-against-target-2"></a>Executar a reprodução de rastreamento no destino 2

Depois de concluir a execução da reprodução de rastreamento no destino 1, você precisa fazer o mesmo em relação ao segundo destino, que representa o ambiente de atualização pretendido.

1. Configure uma reprodução de rastreamento, desta vez usando detalhes associados ao seu ambiente de destino 2.
2. Inicie a reprodução de rastreamento no destino 2.

   Você pode monitorar o processo conforme necessário. Quando a execução da reprodução for concluída, o DEA armazenará os resultados em um arquivo no local especificado.

## <a name="frequently-asked-questions-about-trace-replay"></a>Perguntas frequentes sobre a reprodução de rastreamento

**P: quais permissões de segurança preciso para iniciar uma captura de reprodução no meu servidor de destino?**

- O usuário do Windows que está executando a operação de rastreamento no aplicativo DEA deve ter direitos sysadmin no computador de destino que executa o SQL Server. Esses direitos de usuário são necessários para iniciar um rastreamento.
- A conta de serviço sob a qual o computador de destino que executa o SQL Server está em execução deve ter acesso de gravação ao caminho do arquivo de rastreamento especificado.
- A conta de serviço sob a qual os serviços de cliente do Distributed Replay estão em execução deve ter direitos de usuário para se conectar ao computador de destino que executa o SQL Server e executar consultas.

**P: posso iniciar mais de uma reprodução na mesma sessão?**

Sim, você pode iniciar várias repetições e rastreá-las para conclusão na mesma sessão.

**P: posso iniciar mais de uma reprodução em paralelo?**

Sim, mas não com o mesmo conjunto de computadores selecionado no **controlador mais clientes**. O controlador e os clientes estarão ocupados. Configure um conjunto separado de computadores no **controlador mais o cliente** para iniciar uma reprodução paralela.

**P: quanto tempo uma reprodução geralmente leva para ser concluída?**

Uma reprodução normalmente leva o mesmo período de tempo que o rastreamento de origem, além da quantidade de tempo que leva para pré-processar o rastreamento de origem. No entanto, se os computadores cliente registrados com o controlador não forem suficientes para gerenciar a carga produzida da reprodução, a reprodução poderá levar mais tempo para ser concluída. Você pode registrar até 16 computadores cliente com o controlador.

**P: Qual é o tamanho dos arquivos de rastreamento de destino?**

Os arquivos de rastreamento de destino podem estar entre 5 e 15 vezes o tamanho do rastreamento de origem. O tamanho do arquivo é baseado em quantas consultas são executadas. Por exemplo, os blobs de plano de consulta podem ser grandes. Se as estatísticas dessas consultas forem alteradas com frequência, mais eventos serão capturados.

**P: por que preciso restaurar bancos de dados?**

SQL Server é um sistema de gerenciamento de banco de dados relacional com estado. Para executar corretamente um teste A/B, o estado do banco de dados deve ser mantido sempre. Caso contrário, você poderá ver erros em consultas durante a repetição que não aparecerão na produção. Para evitar esses erros, recomendamos que você faça um backup logo antes da captura de origem. Da mesma forma, é necessário restaurar o backup no computador de destino que executa o SQL Server para evitar erros durante a repetição.

**P: o que significa "Pass%" na página de reprodução?**

A **passagem%** significa que apenas uma porcentagem de consultas foi aprovada. Você pode diagnosticar se o número de erros é esperado. Os erros podem ser esperados ou os erros podem ocorrer porque o banco de dados perdeu sua integridade. Se o valor da **passagem%** não for o esperado, você poderá interromper o rastreamento e examinar o arquivo de rastreamento no SQL Profiler para ver quais consultas não foram bem sucedidos.

**P: como posso examinar os eventos de rastreamento que foram coletados durante a reprodução?**

Abra um arquivo de rastreamento de destino e exiba-o no SQL Profiler. Ou\\, se você quiser fazer modificações na captura de reprodução, todos os scripts de SQL Server estarão disponíveis em C: Arquivos de programas (x86)\\Microsoft Corporation\\assistente para experimentos de banco de dados\\scripts\\StartReplayCapture. Sql.

**P: quais eventos de rastreamento o DEA coleta durante a reprodução?**

O DEA captura eventos de rastreamento que contêm informações relacionadas ao desempenho. A configuração de captura está no script StartReplayCaptureTrace. Sql. Esses eventos são típicos SQL Server eventos de rastreamento listados na [documentação de referência do sp_trace_setevent (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql).

## <a name="troubleshoot-trace-replay"></a>Solucionar problemas de reprodução de rastreamento

**P: por que não consigo me conectar ao computador que está executando o SQL Server?**

- Confirme se o nome do computador que executa o SQL Server é válido. Para confirmar, tente se conectar ao servidor usando SQL Server Management Studio (SSMS).
- Confirme se a configuração do firewall não bloqueia conexões com o computador que executa o SQL Server.
- Confirme se o usuário tem os direitos de usuário necessários.
- Confirme se a conta de serviço do cliente Distributed Replay tem acesso ao computador que está executando o SQL Server.

Você pode obter mais detalhes nos logs em% temp%\\DEA. Se o problema persistir, entre em contato com a equipe do produto.

**P: por que não consigo me conectar ao controlador de Distributed Replay?**

- Verifique se o serviço do controlador de Distributed Replay está em execução no computador do controlador. Para verificar, use as ferramentas de gerenciamento de Distributed Replay (execute `dreplay.exe status -f 1`o comando).
- Se a reprodução for iniciada remotamente:
  - Confirme se o computador que está executando o DEA pode executar ping no controlador com êxito. Confirme se as configurações de firewall permitem conexões de acordo com as instruções na página **Configurar ambiente de reprodução** . Para obter mais informações, consulte o artigo [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017).
  - Verifique se o início remoto DCOM e a ativação remota são permitidos para o usuário do controlador de Distributed Replay.
  - Verifique se os direitos de usuário de acesso remoto DCOM são permitidos para o usuário do controlador de Distributed Replay.

**P: o caminho do arquivo de rastreamento existe em meu computador. Por que o controlador não pode Distributed Replay encontrá-lo?**

Distributed Replay pode acessar apenas os recursos de disco local. Você deve copiar os arquivos de rastreamento de origem para o computador do controlador de Distributed Replay antes de iniciar a reprodução. Além disso, você deve fornecer o caminho na página **nova reprodução** do DEA.

Os caminhos UNC não são compatíveis com Distributed Replay. Caminhos de Distributed Replay devem ser caminhos locais e absolutos para o primeiro arquivo de rastreamento de origem, incluindo a extensão.

**P: por que não consigo procurar arquivos na nova página de reprodução?**

Como não podemos procurar pastas em um computador remoto, procurar arquivos não é útil. É mais eficiente copiar e colar os caminhos absolutos.

**P: comecei a repetir com um rastreamento, mas Distributed Replay não reproduziu nenhum evento. Por?**

Esse problema pode ocorrer porque o arquivo de rastreamento não tem os eventos que podem ser reproduzidos ou tem informações sobre como repetir eventos. Confirme se o caminho do arquivo de rastreamento fornecido aponta para um arquivo de rastreamento de origem. O arquivo de rastreamento de origem é criado usando a configuração fornecida no script StartCaptureTrace. Sql.

**P: Eu vejo "ocorreu um erro inesperado!" ao tentar pré-processar meus arquivos de rastreamento usando o controlador de Distributed Replay SQL Server 2017. Por?**

Esse problema é conhecido na versão RTM do SQL Server 2017. Para obter mais informações, consulte [erro inesperado ao usar o recurso DReplay para reproduzir um rastreamento capturado no SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a).  
  
O problema foi resolvido na atualização cumulativa 1 mais recente para o SQL Server 2017. Baixe a versão mais recente da [atualização cumulativa 1 para SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017).

## <a name="see-also"></a>Confira também

- Para criar um relatório de análise que ajuda você a obter informações sobre as alterações propostas, consulte [criar relatórios](database-experimentation-assistant-create-report.md).
