---
title: Preparar os dados usando o PowerShell (passo a passo) | Microsoft Docs
ms.custom: 
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: "30"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 9ea7df81b4ef2d3bddabdc6c7ff13bf9abba2f6e
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>Preparar os dados usando o PowerShell (passo a passo)

Neste momento, você deve ter o seguinte instalado:

+ SQL Server 2016 R Services
+ SQL Server 2017 Machine Learning Services, com a linguagem R habilitada

Nesta lição, você pode baixar os dados, os pacotes R e os scripts de R usados no passo a passo de um repositório Github. Você pode baixar tudo usando um script do PowerShell para sua conveniência.

Você também precisa instalar alguns pacotes de R adicionais, no servidor e na estação de trabalho de R. As etapas são descritas.

Em seguida, você deve usar um segundo script do PowerShell, RunSQL_R_Walkthrough.ps1, para configurar o banco de dados que é usado para modelar e pontuação. Se o script executa um carregamento em massa dos dados no banco de dados especificar e, em seguida, cria algumas funções SQL e procedimentos armazenados que simplificam as tarefas de ciência de dados.

Vamos começar!

## <a name="1-download-the-data-and-scripts"></a>1. Baixar os dados e scripts

Todo o código necessário foi fornecido em um repositório do GitHub. Você pode usar um script do PowerShell para fazer uma cópia local dos arquivos.

1.  No computador cliente da ciência de dados, abra um prompt de comando do Windows PowerShell como administrador.

2.  Para garantir que você possa executar o script de download sem erro, execute este comando. Ele permite scripts temporariamente sem alterar os padrões do sistema.

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  Execute o comando do PowerShell a seguir para baixar os arquivos de script em um diretório local. Se você não especificar um diretório diferente, por padrão, a pasta `C:\tempR` é criado e salvos de todos os arquivos.
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    Se você deseja salvar os arquivos em outro diretório, edite os valores do parâmetro *DestDir* e especifique uma pasta diferente no computador. Se você digitar um nome de pasta não existir, o script do PowerShell cria a pasta para você.
  
4.  O download pode levar algum tempo. Após ele ser concluído, o console de comando do Windows PowerShell deverá ter a seguinte aparência:
  
    ![Após a conclusão do script do PowerShell](media/rsql-e2e-psscriptresults.PNG "Após a conclusão do script do PowerShell")
  
5.  No console do PowerShell, execute o comando `ls` para exibir uma lista dos arquivos que foram baixados em *DestDir*.  Para obter uma descrição dos arquivos, consulte [o que está incluído](#What-the-Download-Includes).

## <a name="2-install-required-r-packages"></a>2. Instalar pacotes de R necessários

Este passo a passo exige algumas bibliotecas do R que não são instaladas por padrão como parte do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Você deve instalar os pacotes no cliente onde você desenvolve a solução e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador onde você implanta a solução.

### <a name="install-required-packages-on-the-client"></a>Instalar os pacotes necessários no cliente

O script do R baixado inclui os comandos para baixar e instalar esses pacotes.

1. No ambiente do R, abra o arquivo de script, RSQL_R_Walkthrough.R.

2. Realce e execute essas linhas.
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    Alguns pacotes também instalam os pacotes necessários. Ao todo, 32 pacotes são necessários.

### <a name="install-required-packages-on-the-server"></a>Instalar os pacotes necessários no servidor

Há várias maneiras diferentes que você pode instalar pacotes no SQL Server. Por exemplo, o SQL Server fornece um [pacote de gerenciamento](../r/installing-and-managing-r-packages.md) recurso que permite que os administradores de banco de dados cria um repositório de pacote e atribuir os direitos para instalar seus próprios pacotes de usuário. No entanto, se você for um administrador no computador, você pode instalar novos pacotes usando o R, contanto que você instale a biblioteca correta.

> [!NOTE]
> No servidor, **não** instalar em uma biblioteca do usuário, mesmo se for solicitado. Se você instalar uma biblioteca de usuário, a instância do SQL Server não pode localizar ou executar os pacotes. Para saber mais, veja [Instalando novos pacotes de R no SQL Server](../r/install-additional-r-packages-on-sql-server.md).

1. No computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra RGui.exe **como administrador**.  Se você tiver instalado o SQL Server R Services usando os padrões, RGui.exe poderá ser encontrado em C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64.

2.  Em um prompt do R, execute os seguintes comandos do R:
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - Este exemplo usa a função de grep R para pesquisar o vetor de caminhos disponíveis e localize o caminho que inclui "Arquivos de programas". Para obter mais informações, visite [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep).

    - Se você acha que os pacotes já estão instalados, verifique a lista de pacotes instalados executando `installed.packages()`.

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3. Preparar o ambiente usando RunSQL_R_Walkthrough.ps1

Juntamente com os arquivos de dados, scripts de R e scripts T-SQL, o download inclui o script do PowerShell `RunSQL_R_Walkthrough.ps1`. O script executa estas ações:

- Verifica se o SQL Native Client e os utilitários de linha de comando do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão instalados. As ferramentas de linha de comando é necessária para executar o [Utilitário bcp](../../tools/bcp-utility.md), que é usado para o carregamento em massa rápido de dados em tabelas SQL.

- Conecta-se à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa alguns scripts do [!INCLUDE[tsql](../../includes/tsql-md.md)] que configuram o banco de dados e criam as tabelas para o modelo e os dados.

- Executa um script SQL para criar vários procedimentos armazenados.

- Carrega os dados que você baixou anteriormente em uma tabela chamada `nyctaxi_sample`.

- Grava os argumentos novamente no arquivo de script do R para usar o nome do banco de dados especificado.

Execute este script no computador em que você compile a solução: por exemplo, o laptop em que você desenvolve e testar seu código R. Esse computador, que chamaremos de cliente de ciência de dados, deve ser capaz de conectar-se ao computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o protocolo de Pipes Nomeados.

1. Abra uma linha de comando do PowerShell **como administrador**.
  
2.  Procure a pasta em que você baixou os scripts e digite o nome do script, como mostrado abaixo. Pressione ENTER.

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3.  Você será solicitado para cada um dos seguintes parâmetros:
  
    **Nome do servidor de banco de dados**: O nome da instância do SQL Server em que os serviços ou serviços de R de aprendizado de máquina está instalada.

    Dependendo dos requisitos da rede, o nome da instância poderá exigir qualificação com um ou mais nomes de sub-rede.  Por exemplo, se MYSERVER não funcionar, tente myserver.subnet.mycompany.com.
    
    **Nome do banco de dados que você deseja criar**: por exemplo, você pode digitar **Tutorial** ou **Táxi**

    **Nome de usuário**: forneça uma conta que tenha privilégios de acesso a bancos de dados. Há duas opções:
    
    + Digite o nome de um logon SQL que tem privilégios CREATE DATABASE, e forneça a senha do SQL em um prompt sucessivo.
    + Pressione ENTER sem digitar qualquer nome para usar sua própria identidade do Windows e, no prompt protegido, digite sua senha do Windows. O PowerShell não oferece suporte para a inserção de um nome de usuário diferente do Windows.
    + Se você não especificar um usuário válido, o script padrão usando a autenticação integrada do Windows.
    
      > [!WARNING]
      > Quando você usar o prompt no script do PowerShell para fornecer suas credenciais, a senha é gravada no arquivo de script atualizado em texto sem formatação. Edite o arquivo para remover as credenciais imediatamente depois de ter criado os objetos do R necessários.
      
    **Caminho do arquivo csv**: forneça o caminho completo do arquivo de dados. O caminho e nome do arquivo padrão é `C:\tempR\nyctaxi1pct.csv`.
  
4.  Pressione ENTER para executar o script.

    O script deve baixar o arquivo e carregar os dados no banco de dados automaticamente. Isso pode levar algum tempo. Observe as mensagens de status na janela do PowerShell.
      
    Se, importação em massa ou qualquer outra etapa falhar, você poderá carregar os dados manualmente conforme descrito no [solução de problemas](#bkmk_Troubleshooting) seção.

**Resultados (conclusão bem-sucedida)**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

Clique neste link para ir para a próxima lição: [exibir e explorar os dados usando SQL](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>Solução de problemas

Se você tiver problemas com o script do PowerShell, você pode executar todos ou qualquer uma das etapas manualmente, usando as linhas do script do PowerShell como exemplos. Esta seção lista alguns problemas comuns e soluções alternativas.

### <a name="powershell-script-didnt-download-the-data"></a>O script do PowerShell não baixou os dados

Para baixar os dados manualmente, clique com o botão direito do mouse no link a seguir e selecione **Salvar destino como**.

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

Anote o caminho para o arquivo de dados baixado e o nome do arquivo em que os dados foram salvos. É necessário o caminho completo para carregar os dados para a tabela usando **bcp**.

### <a name="unable-to-download-the-data"></a>Não foi possível baixar os dados

O arquivo de dados é grande. Você deve usar um computador que tenha uma conexão de Internet relativamente boa ou o download pode atingir o tempo limite.

### <a name="could-not-connect-or-script-failed"></a>Não foi possível conectar ou ocorreu falha no script

Você poderá receber este erro ao executar um dos scripts: *um erro relativo à rede ou específico da instância ocorreu ao estabelecer conexão com o SQL Server*

+ Verifique a ortografia do nome da instância.
+ Verifique a cadeia de conexão completa.
+ Dependendo dos requisitos da rede, o nome da instância poderá exigir qualificação com um ou mais nomes de sub-rede.  Por exemplo, se MYSERVER não funcionar, tente myserver.subnet.mycompany.com.
+ Verifique se o Firewall do Windows permite conexões pelo SQL Server.
+ Tente registrar seu servidor e certificar-se de que ele permite conexões remotas.
+ Se você estiver usando uma instância nomeada, habilite o SQL Browser para facilitar as conexões.

### <a name="network-error-or-protocol-not-found"></a>Erro de rede ou o protocolo não foi encontrado

+ Verifique se a instância dá suporte a conexões remotas.
+ Certifique-se de que o usuário do SQL especificado possa se conectar remotamente ao banco de dados.
+ Habilite os Pipes Nomeados na instância.
+ Verifique as permissões da conta. A conta especificada pode não ter as permissões para criar um novo banco de dados e carregar os dados.

### <a name="bcp-did-not-run"></a>O bcp não foi executado

+ Verifique se o [utilitário bcp](../../tools/bcp-utility.md) está disponível no computador. Você pode executar o **bcp** de uma janela do PowerShell ou então de um prompt de comando do Windows.
+ Se você receber um erro, adicione o local do utilitário **bcp** à variável de ambiente do sistema PATH e tente novamente.

### <a name="the-table-schema-was-created-but-the-table-has-no-data"></a>O esquema da tabela foi criado, mas não há nenhum dado na tabela

Se o restante do script foi executado sem problemas, você poderá carregar os dados na tabela manualmente, usando o **bcp** na linha de comando, da seguinte maneira:

#### <a name="using-a-sql-login"></a>Usando um logon do SQL

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password>
~~~~

#### <a name="using-windows-authentication"></a>Usando a autenticação do Windows

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T
~~~~

+ O `in` palavra-chave especifica a direção da movimentação de dados.
+ O argumento  **-f** exige que você especifique o caminho completo de um arquivo de formato. Um arquivo de formato é necessário se você usar a opção **in** .
+ Use os argumentos **-U** e **-P** se estiver executando o bcp com um logon SQL.
+ Use o argumento **-T** se estiver usando a autenticação integrada do Windows.

Se o script não carregar os dados, verifique a sintaxe e verifique se o nome do servidor está especificado corretamente para sua rede. Por exemplo, se você estiver se conectando a uma instância nomeada, certifique-se de incluir quaisquer eventuais sub-redes e incluir o nome do computador. Verifique se o logon tem a capacidade de executar os carregamentos em massa.

### <a name="i-want-to-run-the-script-without-prompts"></a>Desejo executar o script sem prompts

Você pode especificar todos os parâmetros em uma única linha de comando, usando este modelo, com valores específicos para o seu ambiente.

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

O exemplo a seguir executa o script usando um logon do SQL:

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   Conecta-se à instância especificada e ao banco de dados usando as credenciais de *SqlUserName*.
-   Obtém os dados do arquivo *C:\temp\nyctaxi1pct.csv*.
-   Carrega os dados para a tabela *dbo.nyctaxi_sample*, no banco de dados *MyDB* na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada *MyServer*.

### <a name="the-data-loaded-but-it-contains-duplicates"></a>Os dados foram carregados, mas eles contêm duplicatas

Se seu banco de dados contiver uma tabela existente de mesmo nome e o mesmo esquema, **bcp** insere uma nova cópia de dados em vez de sobrescrever os dados existentes.

Para evitar dados duplicados, trunca as tabelas existentes antes de executar o script novamente.

## <a name="whats-included-in-the-sample"></a>O que está incluído no exemplo

Quando você baixa os arquivos do repositório GitHub, você obtém o seguinte:

+ Dados em formato CSV; consulte [treinamento e pontuação dados](#bkmk_data) para obter detalhes
+ Um script do PowerShell para preparar o ambiente
+ Um arquivo de formato XML para importar os dados para o SQL Server usando o bcp
+ Vários scripts T-SQL
+ Todo o código do R que você precisa para executar este passo a passo

### <a name="bkmk_data"></a>Treinamento e classificar dados

Os dados são uma amostragem representativa do conjunto de dados de táxi de Nova York, que contém registros de mais de 173 milhões de corridas individuais em 2013, incluindo tarifas e valores de gorjetas pagas por cada corrida. Para facilitar o trabalho com os dados, a equipe de ciência de dados da Microsoft reduziu a resolução para obter apenas 1% dos dados.  Esses dados foram compartilhados em um contêiner do armazenamento de blobs público no Azure, em formato .CSV. A fonte de dados é um arquivo não compactado, apenas em 350 MB.

+ Conjunto de dados público: [NYC táxi e comissão Limousine] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [Criação de modelos do Azure ML no conjunto de dados NYC táxi] (https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/.

### <a name="powershell-and-r-script-files"></a>Arquivos de script do PowerShell e R

+ **RunSQL_R_Walkthrough.ps1** executar esse script em primeiro lugar, usando o PowerShell. Ele chama os scripts SQL para carregar dados no banco de dados.

+ **taxiimportfmt.xml** Um arquivo de definição de formato que é usado pelo utilitário BCP para carregar dados no banco de dados.

+ **RSQL_R_Walkthrough.R** este é o script de R de núcleo que é usado no restante das lições para fazer a análise de dados e modelagem. Ele fornece todo o código do R de que você precisa para explorar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , criar o modelo de classificação e criar gráficos.

### <a name="t-sql-script-files"></a>Arquivos de script T-SQL

O script do PowerShell executa vários [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts na instância do SQL Server. A seguinte tabela lista o [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts e o que fazer.

|Nome do arquivo de script SQL|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|Cria o banco de dados e duas tabelas:<br /><br /> *nyctaxi_sample*: tabela que armazena os dados de treinamento, um exemplo de 1% do conjunto de dados de táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta.<br /><br /> *nyc_taxi_models*: uma tabela usada para armazenar modelos treinados em formato binário.|
|PredictTipBatchMode.sql|Cria um procedimento armazenado que chama um modelo treinado para prever os rótulos das novas observações. Aceita uma consulta como seu parâmetro de entrada.|
|PredictTipSingleMode.sql|Cria um procedimento armazenado que chama um modelo de classificação treinado para prever os rótulos das novas observações. As variáveis das novas observações são passadas como parâmetros na linha.|
|PersistModel.sql|Cria um procedimento armazenado que ajuda a armazenar a representação binária do modelo de classificação em uma tabela do banco de dados.|
|fnCalculateDistance.sql|Cria uma função de valor escalar do SQL que calcula a distância direta entre os locais de embarque e desembarque de passageiros.|
|fnEngineerFeatures.sql|Cria uma função com valor de tabela SQL que cria recursos para treinar o modelo de classificação|

As consultas T-SQL usadas neste passo a passo foram testadas em podem ser executadas como-está em seu código R. No entanto, se você quer realizar mais testes ou desenvolver sua própria solução, recomendamos o uso de um ambiente de desenvolvimento SQL dedicado para testar e ajustar as consultas primeiro, antes de adicioná-las ao código R.

+ A [extensão mssql](https://code.visualstudio.com/docs/languages/tsql) para [Visual Studio Code](https://code.visualstudio.com/) é um ambiente leve e gratuito para executar consultas e que também dá suporte à maioria das tarefas de desenvolvimento de banco de dados.
+ O [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) é uma ferramenta poderosa, mas gratuita fornecida para desenvolvimento e gerenciamento de bancos de dados do SQL Server.

## <a name="next-lesson"></a>Próxima lição

[Exibir e explorar os dados usando R e SQL](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>Lição anterior

[Passo a passo de ciência de dados de ponta a ponta para R e SQL Server](/walkthrough-data-science-end-to-end-walkthrough.md)

[Pré-requisitos para o passo a passo de ciência de dados](walkthrough-prerequisites-for-data-science-walkthroughs.md)
