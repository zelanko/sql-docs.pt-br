---
title: Instalar o SQL Server serviços de Machine Learning (no banco de dados) no Windows | Microsoft Docs
description: R no SQL Server ou Python no SQL Server está disponível quando você instala os serviços de aprendizado de máquina do SQL Server 2017 no Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7f96c2acbca436ff18ccb6a12421d84bda965e4d
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878089"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Instalar serviços no Windows de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partir do SQL Server 2017, R e Python dão suporte para análise no banco de dados é fornecido em serviços do SQL Server Machine Learning, o sucessor [SQL Server R Services](../r/sql-server-r-services.md) introduzido no SQL Server 2016. Bibliotecas de função estão disponíveis em R e Python e executar como script externo em uma instância do mecanismo de banco de dados. 

Este artigo explica como instalar o componente de aprendizado de máquina executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de instalação e seguir as instruções na tela.

## <a name="bkmk_prereqs"> </a> Lista de verificação de pré-instalação

+ Instalação do 2017 (ou superior) SQL Server será necessária se você deseja instalar os serviços de Machine Learning com o suporte de linguagem R, Python ou Java. Se em vez disso, você tiver a mídia de instalação do SQL Server 2016, você pode instalar [SQL Server 2016 R Services (no banco de dados)](sql-r-services-windows-install.md) para obter suporte à linguagem R.

+ Uma instância do mecanismo de banco de dados é necessária. Você não pode instalar apenas recursos de R ou Python, embora você pode adicioná-los incrementalmente a uma instância existente.

- Instalar serviços de Machine Learning é *não tem suporte* em um cluster de failover no SQL Server 2017. No entanto, ele *há suporte para* com o SQL Server de 2019. 
 
+ Não instale os serviços de aprendizado de máquina em um controlador de domínio. A parte de serviços de Machine Learning da instalação falhará.

+ Não instale **recursos compartilhados** > **Machine Learning Server (autônomo)** no mesmo computador que está executando uma instância no banco de dados. Um servidor autônomo competirão pelos mesmos recursos, prejudicando o desempenho de ambas as instalações.

+ Instalação lado a lado com outras versões do R e Python tem suporte mas não é recomendada. Ele é compatível porque a instância do SQL Server usa suas próprias cópias das distribuições de R e Anaconda do código-fonte aberto. Mas ele não é recomendado porque executando o código que usa o R e Python no computador do SQL Server fora do SQL Server pode causar vários problemas:
    
  + Você usa uma biblioteca diferente e executável diferente e obter resultados diferentes, do que quando você estiver executando no SQL Server.
  + Scripts de R e Python em execução em bibliotecas externas não podem ser gerenciados pelo SQL Server, levando à contenção de recursos.
  
> [!IMPORTANT]
> Após a conclusão da instalação, certifique-se de concluir as etapas de pós-configuração descritas neste artigo. Essas etapas incluem a habilitação do SQL Server usar scripts externos e adicionando as contas necessárias para o SQL Server executar trabalhos de R e Python em seu nome. Alterações de configuração geralmente requerem uma reinicialização da instância ou uma reinicialização do serviço Launchpad.

## <a name="get-the-installation-media"></a>Obtenha a mídia de instalação

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Executar a instalação

Para instalações locais, você deve executar a Instalação como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e de execução no compartilhamento remoto.

1. Inicie o Assistente de instalação do SQL Server 2017. Você pode baixar 
  
2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.

   ![Instalar o Machine Learning Services no banco de dados](media/2017setup-installation-page-mlsvcs.PNG)
   
3. Na página **Seleção de Recursos** , selecione estas opções:
  
    -   **Serviços do Mecanismo de Banco de Dados**
  
         Para usar o R e Python com o SQL Server, você deve instalar uma instância do mecanismo de banco de dados. Você pode usar um padrão ou uma instância nomeada.
  
    -   **Serviços de Machine Learning (no banco de dados)**
  
         Esta opção instala os serviços de banco de dados que dão suporte a R e execução de script do Python.

    -   **R**

        Marque esta opção para adicionar os pacotes Microsoft R, interpretador e r de código-fonte aberto. 

    -   **Python**

        Marque esta opção para adicionar os pacotes do Python de Microsoft, o executável do Python 3.5 e selecione bibliotecas da distribuição Anaconda.
        
        ![Opções para R e Python de recursos](media/2017setup-features-page-mls-rpy.png "opções de configuração para Python")

        > [!NOTE]
        > 
        > Não selecione a opção para **Machine Learning Server (autônomo)**. A opção de instalar o Machine Learning Server sob **recursos compartilhados** é destinado para uso em um computador separado.

4. Sobre o **consentimento para instalar o R** página, selecione **Accept**. Este contrato de licença aborda o Microsoft R Open, que inclui uma distribuição dos pacotes de base de R de código-fonte aberto e ferramentas, junto com pacotes de R aprimorados e provedores de conectividade da equipe de desenvolvimento da Microsoft.

5. Sobre o **consentimento para instalar o Python** página, selecione **Accept**. O contrato de licença de software livre de Python também aborda o Anaconda e ferramentas relacionadas, além de algumas novas bibliotecas de Python da equipe de desenvolvimento da Microsoft.
     
     ![Contrato de licença do Python](media/2017setup-python-license.png "contrato para o Python de licença")
  
    > [!NOTE]
    >  Se o computador que está usando não tiver acesso à internet, você pode pausar o programa de instalação neste momento para baixar os instaladores separadamente. Para obter mais informações, consulte [instalar componentes de aprendizado de máquina sem acesso à internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Selecione **Accept**, aguarde até que o **próxima** botão se torna ativo e, em seguida, selecione **próxima**.
  
6. Sobre o **pronto para instalar** , verifique se que essas seleções são incluídas e selecione **instalar**.
  
    + Serviços do Mecanismo de Banco de Dados
    + Serviços de Machine Learning (No Banco de Dados)
    + R, Python ou ambos

    Anote o local da pasta no caminho `..\Setup Bootstrap\Log` onde os arquivos de configuração são armazenados. Quando a instalação for concluída, você pode examinar os componentes instalados no arquivo de resumo.

7. Após a instalação for concluída, se você for instruído a reiniciar o computador, faça isso agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações, consulte [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Habilitar a execução do script

1. Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Você pode baixar e instalar a versão apropriada nesta página: [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > Você também pode experimentar a versão de visualização da [Studio do Azure Data](../../azure-data-studio/what-is.md), que oferece suporte a tarefas administrativas e consultas no SQL Server.
  
2. Conecte-se à instância onde você instalou os serviços de Machine Learning, clique em **nova consulta** para abrir uma janela de consulta e execute o seguinte comando:

   ```SQL
   sp_configure
   ```

    O valor da propriedade `external scripts enabled`, deve ser **0** neste momento. Isso ocorre porque o recurso é desativado por padrão. O recurso deve ser habilitado explicitamente por um administrador antes de executar scripts R ou Python.
    
3.  Para habilitar o recurso de script externo, execute a seguinte instrução:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Se você já tiver habilitado o recurso para a linguagem R, não execute reconfigurar uma segunda vez para o Python. A plataforma de extensibilidade subjacente dá suporte a ambas as linguagens.

## <a name="restart-the-service"></a>Reinicie o serviço.

Quando a instalação for concluída, reinicie o mecanismo de banco de dados antes de continuar para a próxima, permitindo a execução do script.

Reiniciar o serviço também automaticamente reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

Você pode reiniciar o serviço usando o botão direito do mouse **reinicie** comando para a instância no SSMS ou usando o **Services** painel no painel de controle ou usando [SQL Server Configuration Manager ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Verifique a instalação

Verificar o status de instalação da instância na [relatórios personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md) ou logs de instalação.

Use as etapas a seguir para verificar se todos os componentes usados para iniciar o script externo estão em execução.

1. No SQL Server Management Studio, abra uma nova janela de consulta e execute o seguinte comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    O **run_value** agora deve ser definido como 1.
    
2. Abra o **Services** painel ou o SQL Server Configuration Manager e verifique se **Launchpad do SQL Server service** está em execução. Você deve ter um serviço para cada instância do mecanismo de banco de dados que tem o R ou Python instalado. Para obter mais informações sobre o serviço, consulte [Extensibility framework](../concepts/extensibility-framework.md). 
   
3. Se o Launchpad estiver em execução, você poderá executar scripts R e Python simples para verificar se os tempos de execução de scripts externos podem se comunicar com o SQL Server.

   Abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e, em seguida, executar um script como o seguinte:
    
    + Para R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Para Python
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

 **Resultados**

    O script pode demorar um pouco enquanto executar na primeira vez que o tempo de execução do script externo é carregado. Os resultados devem ser algo parecido com isto:

    | hello |
    |----|
    | 1|


> [!NOTE]
> Colunas ou títulos usados no script do Python não forem retornados, por design. Para adicionar nomes de coluna de saída, você deve especificar o esquema para o conjunto de dados de retorno. Faça isso usando o parâmetro com resultados do procedimento armazenado, as colunas de nomenclatura e especificando o tipo de dados SQL.
> 
> Por exemplo, você pode adicionar a seguinte linha para gerar um nome arbitrário de coluna: `WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar atualizações

É recomendável que você aplique a atualização cumulativa mais recente para o mecanismo de banco de dados e componentes de aprendizado de máquina.

Em dispositivos conectados à internet, as atualizações cumulativas são geralmente aplicadas por meio do Windows Update, mas você também pode usar as etapas abaixo para atualizações de controlado. Quando você aplicar a atualização para o mecanismo de banco de dados, a instalação extrai as atualizações cumulativas para quaisquer recursos de R ou Python instalados na mesma instância. 

Em servidores desconectados, são necessárias etapas adicionais. Para obter mais informações, consulte [instalar em computadores sem acesso à internet > Aplicar atualizações cumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Começar com uma instância de linha de base já instalada: versão inicial do SQL Server 2017

2. Vá para a lista de atualização cumulativa: [atualiza do SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Selecione a atualização cumulativa mais recente. Um executável é baixado e extraído automaticamente.

4. Execute a instalação. Aceite os termos de licenciamento e, na página de seleção de recursos, analise os recursos para os quais as atualizações cumulativas são aplicadas. Você deve ver todos os recursos instalados para a instância atual, incluindo recursos de aprendizado de máquina. A instalação baixará os arquivos CAB necessários para atualizar todos os recursos.

  ![](media/cumulative-update-feature-selection.png)

5. Prossiga com o assistente, aceitando os termos de licenciamento para distribuições do R e Python. 

## <a name="additional-configuration"></a>Configuração adicional

Se a etapa de verificação de script externo foi bem-sucedida, você pode executar comandos de R ou Python do SQL Server Management Studio, Visual Studio Code ou qualquer outro cliente que pode enviar instruções T-SQL para o servidor.

Se você obteve um erro ao executar o comando, examine as etapas de configuração adicionais nesta seção. Talvez seja necessário fazer configurações adicionais de apropriado para o serviço ou o banco de dados.

No nível de instância, configurações adicionais podem incluir:

* [Configuração do firewall para serviços do SQL Server Machine Learning](../../advanced-analytics/security/firewall-configuration.md)
* [Habilite os protocolos de rede adicionais](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexões remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

Banco de dados, talvez você precise as atualizações de configuração a seguir:

* [Conceder aos usuários permissão para serviços do SQL Server Machine Learning](../../advanced-analytics/security/user-permission.md)
* [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> Se a configuração adicional é necessária depende de seu esquema de segurança, onde você instalou o SQL Server e como você espera que os usuários para se conectar ao banco de dados e executar scripts externos.

## <a name="suggested-optimizations"></a>Otimizações sugeridas

Agora que você tem tudo funcionando, você também poderá otimizar o servidor para oferecer suporte ao aprendizado de máquina ou modelos pré-treinados de instalação.

### <a name="add-more-worker-accounts"></a>Adicionar mais contas de trabalho

Se você espera que muitos usuários executarão scripts simultaneamente, você pode aumentar o número de contas de trabalho que são atribuídos ao serviço Launchpad. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços do SQL Server Machine Learning](../administration/modify-user-account-pool.md).

### <a name="optimize-the-server-for-script-execution"></a>Otimizar o servidor para execução de script

As configurações padrão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação destinam-se para otimizar o equilíbrio entre o servidor para uma variedade de serviços que têm suporte pelo mecanismo de banco de dados, que pode incluir a extração, transformação e carregamento (ETL) de processos, relatórios, auditoria, e aplicativos que usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados. Portanto, sob as configurações padrão, você pode encontrar recursos de aprendizagem de máquina, às vezes, são restritos ou limitados, especialmente em operações com uso intensivo de memória.

Para garantir que os trabalhos de aprendizado de máquina são priorizados e tenham os recursos apropriados, é recomendável que você use o administrador de recursos do SQL Server para configurar um pool de recursos externos. Você também poderá alterar a quantidade de memória alocada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados ou aumentar o número de contas que são executados sob o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar um pool de recursos para gerenciamento de recursos externos, consulte [criar um pool de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para alterar a quantidade de memória reservada para o banco de dados, consulte [opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para alterar o número de contas do R que pode ser iniciado por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar o pool de conta de usuário para o machine learning](../administration/modify-user-account-pool.md).

Se você estiver usando o Standard Edition e tiver o Resource Governor, você pode usar o Extended Events e exibições de gerenciamento dinâmico (DMVs), bem como monitoramento, para ajudar a gerenciar os recursos do servidor de eventos do Windows. Para obter mais informações, consulte [monitoramento e gerenciamento de serviços de R](../r/managing-and-monitoring-r-solutions.md) e [monitorando e gerenciando serviços Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar pacotes R adicionais

As soluções de R que você cria para o SQL Server podem chamar funções básicas de R, funções de pacotes de proprietários instalados com o SQL Server e pacotes de R de terceiros compatível com a versão de software livre R instalado pelo SQL Server.

Pacotes que você desejar usar do SQL Server deverão ser instalados na biblioteca padrão usada pela instância. Se você tiver uma instalação separada do R no computador, ou se você tiver instalado pacotes em bibliotecas do usuário, você não poderá usar os pacotes do T-SQL.

O processo para instalar e gerenciar pacotes de R é diferente no SQL Server 2016 e SQL Server 2017. No SQL Server 2016, um administrador de banco de dados deve instalar os pacotes de R que os usuários precisam. No SQL Server 2017, você pode configurar grupos de usuários para compartilhar pacotes em um nível por banco de dados ou configurar as funções de banco de dados para permitir que os usuários instalem seus próprios pacotes. Para obter mais informações, consulte [instalar novos pacotes de R no SQL Server](../r/install-additional-r-packages-on-sql-server.md).


## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores do R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem aprender como usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise de no banco de dados para desenvolvedores do Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).
