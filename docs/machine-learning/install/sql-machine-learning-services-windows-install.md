---
title: Instalar no Windows
description: Saiba como instalar os Serviços de Machine Learning do SQL Server no Windows. Você pode usar Serviços do Machine Learning (no banco de dados) para executar scripts de Python e R no banco de dados.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 02/29/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017'
ms.openlocfilehash: 9df3f0d56e3d210389110cdf155bd79a32c7c978
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471187"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-windows"></a>Instalar Serviços de Machine Learning do SQL Server (R e Python) no Windows

[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Saiba como instalar os Serviços de Machine Learning do SQL Server no Windows. Você pode usar Serviços do Machine Learning (no banco de dados) para executar scripts de Python e R no banco de dados.

## <a name="pre-install-checklist"></a><a name="bkmk_prereqs"> </a> Lista de verificação pré-instalação

+ Uma instância do mecanismo de banco de dados é necessária. Não é possível instalar somente os recursos do R ou do Python, embora seja possível adicioná-los incrementalmente a uma instância existente.

+ Para continuidade dos negócios, os [grupos de disponibilidade Always On](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) são compatíveis com os Serviços de Machine Learning. Instale os Serviços de Machine Learning e configure os pacotes em cada nó.

+ *Não há suporte* para a instalação dos Serviços de Machine Learning em uma [FCI (Instância do Cluster de Failover) Always On](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) no SQL Server 2017. Ela tem suporte com o SQL Server 2019 e posteriores.
 
+ Não instale os Serviços de Machine Learning em um controlador de domínio. A parte dos Serviços de Machine Learning da instalação falhará.

+ Não instale **Recursos Compartilhados** > **Machine Learning Server (Autônomo)** no mesmo computador que executa uma instância do banco de dados. Um servidor autônomo competirá pelos mesmos recursos, diminuindo o desempenho das duas instalações.

+ A instalação lado a lado com outras versões do R e do Python é compatível, mas não recomendada. Ela é compatível porque a instância do SQL Server usa as próprias cópias das distribuições do R e do Anaconda de software livre. Não é recomendável porque a execução de código que usa R e Python no computador SQL Server fora do SQL Server pode gerar vários problemas:
    
  + Usar uma biblioteca e arquivos executáveis diferentes criará resultados inconsistentes do que o que você está executando no SQL Server.
  + Scripts de R e Python executados em bibliotecas externas não podem ser gerenciados pelo SQL Server, o que leva à contenção de recursos.

::: moniker range=">=sql-server-ver15"
> [!NOTE]
> Os Serviços de Machine Learning são instalados por padrão nos **Clusters de Big Data do SQL Server**. Caso use um **Cluster de Big Data**, não será preciso seguir as etapas deste artigo. Para obter mais informações, confira [Usar Serviços de Machine Learning (Python e R) em Clusters de Big Data](../../big-data-cluster/machine-learning-services.md).
::: moniker-end

> [!IMPORTANT]
> Após a conclusão da instalação, conclua as etapas de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação do SQL Server para usar scripts externos e a adição de contas necessárias para o SQL Server executar trabalhos do R e do Python em seu nome. Geralmente, as alterações na configuração exigem uma reinicialização da instância ou do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

::: moniker range="=sql-server-2017"
Para saber mais sobre quais edições do SQL Server são compatíveis com as integrações de Python e R com os Serviços de Machine Learning, confira [Edições e recursos compatíveis com o SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).
::: moniker-end

::: moniker range="=sql-server-ver15"
Para saber mais sobre quais edições do SQL Server são compatíveis com as integrações de Python e R com os Serviços de Machine Learning, confira [Edições e recursos compatíveis com o SQL Server 2019 (15.x)](../../sql-server/editions-and-components-of-sql-server-version-15.md).
::: moniker-end

## <a name="run-setup"></a>Executar a instalação

Em instalações locais, você deve executar a instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o assistente de instalação do SQL Server.
  
1. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.

   ::: moniker range="=sql-server-2017"
   ![Nova instalação autônoma do SQL Server](media/2017setup-installation-page-mlsvcs.png)
   ::: moniker-end

   ::: moniker range="=sql-server-ver15"
   ![Nova instalação autônoma do SQL Server](media/2019setup-installation-page-mlsvcs.png)
   ::: moniker-end

1. Na página **Seleção de Recursos** , selecione estas opções:

   ::: moniker range="=sql-server-2017"

   - **Serviços do Mecanismo de Banco de Dados**
     
     Para usar o R e o Python com o SQL Server, você deverá instalar uma instância do mecanismo de banco de dados. Você pode usar uma instância padrão ou nomeada.

   - **Serviços de Machine Learning (no banco de dados)**
     
     Esta opção instala os serviços de banco de dados que dão suporte à execução de scripts R e Python.

   ::: moniker-end

   ::: moniker range="=sql-server-ver15"

   - **Serviços do Mecanismo de Banco de Dados**
     
     Para usar o R ou o Python com o SQL Server, você deverá instalar uma instância do mecanismo de banco de dados. Você pode usar uma instância padrão ou nomeada.

   - **Serviços de Machine Learning (no banco de dados)**
     
     Esta opção instala os serviços de banco de dados que dão suporte à execução de scripts R e Python.

   ::: moniker-end

   - **R**
     
     Marque esta opção para adicionar os pacotes do Microsoft R, o interpretador e o R de software livre. 
     
   - **Python**
     
     Marque esta opção para adicionar os pacotes do Microsoft Python e o executável do Python 3.5. Depois, selecione as bibliotecas da distribuição do Anaconda.
     
   ::: moniker range="=sql-server-ver15"
   Para saber mais sobre como instalar e usar o Java, confira [Instalar extensões de linguagem do SQL Server no Windows](../../language-extensions/install/windows-java.md).
   ::: moniker-end
   
   ::: moniker range="=sql-server-2017"
   ![Opções de recurso para o R e o Python](media/2017setup-features-page-mls-rpy.PNG "Opções de instalação para R e Python")
   ::: moniker-end
   
   ::: moniker range="=sql-server-ver15"
   ![Opções de recurso para o R e o Python](media/2019setup-features-page-mls-rpy.png "Opções de instalação para R e Python")
   ::: moniker-end
   
   > [!NOTE]
   > 
   > Não selecione a opção do **Machine Learning Server (Autônomo)** . A opção de instalar o Machine Learning Server em **Recursos Compartilhados** destina-se a ser usada em um computador separado.

::: moniker range="=sql-server-2017"

4. Na página **Consentimento para instalar o Microsoft R Open**, selecione **Aceitar** e **Avançar**. 

O contrato de licença abrange:
+ Microsoft R Open
+ Pacotes e ferramentas de base do R de software livre
+ Pacotes R aprimorados e provedores de conectividade da equipe de desenvolvimento da Microsoft.

1. Na página **Consentimento para instalar o Python**, selecione **Aceitar** e depois **Avançar**. O contrato de licenciamento de software livre do Python também abrange o Anaconda e as ferramentas relacionadas, além de algumas novas bibliotecas do Python da equipe de desenvolvimento da Microsoft.

   > [!NOTE]
   >  Se o computador usado não tiver acesso à Internet, você poderá pausar a instalação neste ponto para baixar os instaladores separadamente. Para obter mais informações, confira [Instalar componentes de machine learning sem acesso à Internet](../install/sql-ml-component-install-without-internet-access.md).

1. Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e selecione **Instalar**.
  
   + Serviços do Mecanismo de Banco de Dados
   + Serviços de Machine Learning (No Banco de Dados)
   + R ou Python ou os dois

   Observe a localização da pasta no caminho `..\Setup Bootstrap\Log` em que os arquivos de configuração são armazenados. Quando a instalação for concluída, você poderá examinar os componentes instalados no arquivo de Resumo.

1. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

::: moniker-end

::: moniker range="=sql-server-ver15"

1. Na página **Consentimento para instalar o Microsoft R Open**, selecione **Aceitar** e **Avançar**. Este contrato de licença abrange o Microsoft R Open, que inclui uma distribuição de pacotes e ferramentas base do R de software livre, junto com pacotes avançados do R e provedores de conectividade da equipe de desenvolvimento da Microsoft.

2. Na página **Consentimento para instalar o Python**, selecione **Aceitar** e depois **Avançar**. O contrato de licenciamento de software livre do Python também abrange o Anaconda e as ferramentas relacionadas, além de algumas novas bibliotecas do Python da equipe de desenvolvimento da Microsoft.

3. Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e selecione **Instalar**.
  
   + Serviços do Mecanismo de Banco de Dados
   + Serviços de Machine Learning (No Banco de Dados)
   + R e/ou Python

   Observação da localização da pasta no caminho `..\Setup Bootstrap\Log` em que os arquivos de configuração são armazenados. Quando a instalação for concluída, você poderá examinar os componentes instalados no arquivo de Resumo.

4. Após a conclusão da instalação, se você receber instruções para reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a instalação. Para saber mais, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).

::: moniker-end

## <a name="set-environment-variables"></a>Definir variáveis de ambiente

Somente para a integração de recursos do R, é necessário definir a variável de ambiente **MKL_CBWR** para [garantir a saída consistente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dos cálculos da Intel MKL (Math Kernel Library).

1. No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.

2. Crie uma variável de usuário ou do sistema. 

   + Defina o nome da variável como `MKL_CBWR`
   + Defina o valor da variável como `AUTO`

Esta etapa requer uma reinicialização do servidor. Se estiver prestes a habilitar a execução de script, você poderá manter a reinicialização até que todo o trabalho de configuração seja concluído.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Habilitar a execução do script

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [Baixe o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).
    > 
    > Você também pode usar o [Azure Data Studio](../../azure-data-studio/what-is.md), que dá suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância em que você instalou os Serviços de Machine Learning, clique em **Nova Consulta** para abrir uma janela de consulta e execute o seguinte comando:

    ```sql
    sp_configure
    ```

    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. O recurso é desativado por padrão. O recurso precisa ser habilitado explicitamente por um administrador antes que seja possível executar scripts R ou Python.
    
3.  Para habilitar o recurso de script externo, execute a instrução a seguir:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Se você já tiver habilitado o recurso para a linguagem R, não execute a reconfiguração uma segunda vez para o Python. A plataforma de extensibilidade subjacente dá suporte às duas linguagens.

## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação estiver concluída, reinicie o mecanismo de banco de dados.

Reiniciar o serviço também reinicia automaticamente o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] relacionado.

Você pode reiniciar o serviço usando o clique com o botão direito do mouse no comando **Reiniciar** para a instância no SSMS ou usando o painel **Serviços** no Painel de Controle ou usando o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
   ```sql
   EXECUTE sp_configure  'external scripts enabled'
   ```

   O **run_value** está definido como 1.
    
2. Abra o painel **Serviços** ou o SQL Server Configuration Manager e verifique se o **serviço SQL Server Launchpad** está em execução. Você deve ter um serviço para toda instância do mecanismo de banco de dados que tem o R ou o Python instalados. Para obter mais informações sobre o serviço, confira [Estrutura de extensibilidade](../concepts/extensibility-framework.md). 
   
3. Se o Launchpad estiver em execução, você deverá executar scripts R e Python simples para verificar se os runtimes de script externo podem se comunicar com o SQL Server.

   Abra uma nova janela **Consulta** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e, em seguida, execute um script como o seguinte:
   + Para R
   
     ```sql
     EXEC sp_execute_external_script  @language =N'R',
     @script=N'
     OutputDataSet <- InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
     
   + Para o Python
     
     ```sql
     EXEC sp_execute_external_script  @language =N'Python',
     @script=N'
     OutputDataSet = InputDataSet;
     ',
     @input_data_1 =N'SELECT 1 AS hello'
     WITH RESULT SETS (([hello] int not null));
     GO
     ```
   
   **Resultados**

   Na primeira vez que o runtime de script externo for carregado, o script poderá demorar um pouco para ser executado. Os resultados devem ser semelhantes a estes:

   | hello |
   |----|
   | 1|

> [!NOTE]
> Colunas ou cabeçalhos usados no script Python não são retornados automaticamente. Para adicionar nomes de coluna para a saída, você deve especificar o esquema para o conjunto de dados de retorno. Faça isso usando o parâmetro WITH RESULTS do procedimento armazenado, nomeando as colunas e especificando o tipo de dados SQL.
>
> Por exemplo, você pode adicionar a linha a seguir para gerar um nome de coluna arbitrário: `WITH RESULT SETS ((Col1 AS int))`

::: moniker range="=sql-server-2017"
<!-- There are no updates yet available for 2019, and there's no 2019 update list site. When updates become available, add 2019 information to this section. -->

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

Recomendamos que você aplique a atualização cumulativa mais recente aos componentes do mecanismo de banco de dados e de aprendizado de máquina.

Em dispositivos conectados à Internet, as atualizações cumulativas são normalmente aplicadas por meio do Windows Update, mas você também pode usar as etapas abaixo para atualizações controladas. Quando você aplica a atualização ao mecanismo de banco de dados, a instalação obtém as atualizações cumulativas para recursos de R ou Python que você tenha instalado na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, confira [Instalar em computadores sem acesso à Internet > Aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comece com uma instância de linha de base já instalada: Versão inicial do SQL Server 2017

2. Acesse a lista de atualizações cumulativas: [Atualizações mais recentes do Microsoft SQL Server](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

3. Selecione a atualização cumulativa mais recente. Um executável é baixado e extraído automaticamente.

4. Execute a instalação. Aceite os termos de licenciamento e, na página seleção de recursos, examine os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo os recursos de aprendizado de máquina. A instalação baixa os arquivos CAB necessários para atualizar todos os recursos.

   ![Resumo dos recursos instalados](media/cumulative-update-feature-selection.png)

5. Continue com o assistente, aceitando os termos de licenciamento para distribuições de R e Python. 

::: moniker-end

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo tiver sido bem-sucedida, você poderá executar comandos do R ou do Python por meio do SQL Server Management Studio, do Azure Data Studio, do Visual Studio Code ou de qualquer outro cliente que possa enviar instruções T-SQL para o servidor.

Se você receber um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário realizar configurações apropriadas adicionais para o serviço ou banco de dados.

No nível da instância, a configuração adicional pode incluir:

* [Configuração de firewall para os Serviços de Machine Learning do SQL Server](../../machine-learning/security/firewall-configuration.md)
* [Habilitar protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Criar um logon para SQLRUserGroup](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)
* [Gerenciar cotas de disco](/windows/desktop/fileio/managing-disk-quotas) para evitar que scripts externos executem tarefas que esgotam o espaço em disco

::: moniker range=">=sql-server-ver15"
No SQL Server 2019 no Windows, o mecanismo de isolamento foi alterado. Esse mecanismo afeta **SQLRUserGroup**, regras de firewall, permissão de arquivo e autenticação implícita. Para obter mais informações, confira [Alterações no isolamento para os Serviços de Machine Learning](sql-server-machine-learning-services-2019.md).
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

No banco de dados, talvez você precise das seguintes atualizações de configuração:

* [Conceder aos usuários permissão para os Serviços de Machine Learning do SQL Server](../../machine-learning/security/user-permission.md)

> [!NOTE]
> A necessidade de configuração adicional depende do seu esquema de segurança, de onde você instalou o SQL Server e como você espera que os usuários se conectem ao banco de dados e executem scripts externos.

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que tudo está funcionando, talvez convenha também otimizar o servidor para compatibilidade com aprendizado de máquina ou então instalar um modelo de machine learning pré-treinado.

::: moniker range="=sql-server-2017"
### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você esperar que vários usuários executem scripts simultaneamente, aumente o número de contas de trabalho atribuídas ao serviço Launchpad. Para obter mais informações, confira a [execução simultânea da escala de scripts externos nos Serviços de Machine Learning do SQL Server](../administration/scale-concurrent-execution-external-scripts.md).
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>Otimizar o servidor para execução de script

As configurações padrão da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinam-se a otimizar o equilíbrio do servidor para uma variedade de serviços compatíveis com o mecanismo de banco de dados, que podem incluir processos ETL (incluir, transformar e carregar), relatórios, auditoria e aplicativos que usam os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nas configurações padrão, os recursos de aprendizado de máquina são algumas vezes restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para verificar se os trabalhos de machine learning são priorizados e têm os recursos apropriados, recomendamos que você use o SQL Server Resource Governor para configurar um pool de recursos externo. Talvez convenha também alterar a quantidade de memória alocada ao mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou aumentar o número de contas executadas no serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].

- Para configurar um pool de recursos para o gerenciamento de recursos externos, confira [Criar um pool de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, confira [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas do R que podem ser iniciadas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], confira [Dimensionar a execução simultânea de scripts externos nos Serviços de Machine Learning do SQL Server](../administration/scale-concurrent-execution-external-scripts.md).

Se estiver usando a Edição Standard e não tiver o Resource Governor, você poderá usar DMVs (Exibições de Gerenciamento Dinâmico) e Eventos Estendidos, assim como o monitoramento de eventos do Windows, para ajudar a gerenciar os recursos do servidor.

### <a name="install-additional-python-and-r-packages"></a>Instalar pacotes adicionais do Python e do R

As soluções Python e R que você cria para SQL Server podem chamar funções básicas, funções dos pacotes proprietários instalados com o SQL Server e pacotes de terceiros compatíveis com a versão do Python e do R de software livre instalados pelo SQL Server.

Os pacotes do SQL Server que você desejar usar deverão ser instalados na biblioteca padrão usada pela instância. Se tiver uma instalação separada do Python ou do R no computador ou se tiver instalado pacotes em bibliotecas do usuário, você não poderá usar os pacotes do T-SQL.

Para instalar e gerenciar pacotes adicionais, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, confira [Instalar pacotes do Python](../package-management/install-additional-python-packages-on-sql-server.md) e [Instalar novos pacotes do R](../package-management/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server](../tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Tutorial do Python: Categorizar clientes que usam cluster K-means com Serviços de Machine Learning do SQL Server](../tutorials/python-clustering-model.md)

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Início Rápido: Executar o R no T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../tutorials/r-taxi-classification-introduction.md)