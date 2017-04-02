---
title: "Li&#231;&#227;o 1: Preparar os dados (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 29
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 25
---
# Li&#231;&#227;o 1: Preparar os dados (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
Para se preparar para este passo a passo, você precisará fazer o seguinte:

1. Baixe os dados e todos os scripts de R usados no passo a passo. Um script do PowerShell é fornecido para simplificar o download do GitHub.   

2. Baixe e instale alguns pacotes do R adicionais, no servidor e na estação de trabalho do R.  

3. Prepare o ambiente, incluindo o banco de dados e os dados usados para modelagem e pontuação.
 
    Para isso, você usará um segundo script do PowerShell, RunSQL_R_Walkthrough.ps1.
    O script configura o banco de dados e carrega os dados na tabela especificada.  Ele também cria algumas funções SQL e procedimentos armazenados que simplificam tarefas de ciência de dados. 
 

## <a name="1-download-the-data-and-scripts"></a>1. Baixar os dados e os scripts  
Todo o código que será necessário para concluir este passo a passo foi fornecido em um repositório GitHub. Você pode usar um script do PowerShell para fazer uma cópia local dos arquivos.  
  
#### <a name="to-download-all-scripts-using-powershell"></a>Para baixar todos os scripts usando o PowerShell  
  
1.  No computador cliente da ciência de dados, abra um prompt de comando do Windows PowerShell como administrador.  
  
2.  Se você não executou o PowerShell antes nesta instância ou se não tem permissão para executar scripts, pode ocorrer um erro. Neste caso, execute este comando antes de executar o script, para permitir scripts temporariamente sem alterar os padrões do sistema.  
  
    ```  
    Set-ExecutionPolicy Unrestricted -Scope Process -Force  
    ```  
  
3.  Execute o comando a seguir para baixar os arquivos de script em um diretório local. Se você não especificar outro diretório, por padrão, a pasta c:\tempR será criada e todos os arquivos serão salvos nela.  
  
    ```  
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'  
  
    ```  
  
    Se você deseja salvar os arquivos em outro diretório, edite os valores do parâmetro *DestDir* e especifique uma pasta diferente no computador. Se você especificar um nome de pasta que não existe, o script do PowerShell criará a pasta para você.  
  
4.  O console de comando do Windows PowerShell deve ser parecido com este após a conclusão do download:  
  
    ![After completion of PowerShell script](../../advanced-analytics/r-services/media/rsql-e2e-psscriptresults.PNG "After completion of PowerShell script")  
  
5.  No console do PowerShell, execute o comando `ls` para exibir uma lista dos arquivos que foram baixados em *DestDir*.  Para obter uma lista e descrição dos arquivos, veja [O que está incluído](#What-the-Download-Includes).
  
## <a name="2-install-required-packages"></a>2. Instalar os pacotes necessários  
Este passo a passo exige algumas bibliotecas do R que não são instaladas por padrão como parte do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. É necessário instalar os pacotes no cliente em que você desenvolverá a solução e no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você implantará a solução.  
  
### <a name="install-required-packages-on-the-client"></a>Instalar os pacotes necessários no cliente  
O script do R baixado inclui os comandos para baixar e instalar esses pacotes.  
  
1.  No ambiente do R, abra o arquivo de script, RSQL_R_Walkthrough.R.  
  
2.  Realce e execute essas linhas.  
  
    ```  
    # Install required R libraries for this walkthrough if they are not installed.   
  
    if (!('ggmap' %in% rownames(installed.packages()))){  
      install.packages('ggmap')  
    }  
    if (!('mapproj' %in% rownames(installed.packages()))){  
      install.packages('mapproj')  
    }  
    if (!('ROCR' %in% rownames(installed.packages()))){  
      install.packages('ROCR')  
    }  
    if (!('RODBC' %in% rownames(installed.packages()))){  
      install.packages('RODBC')  
    }  
    ```  
  
### <a name="install-required-packages-on-the-server"></a>Instalar os pacotes necessários no servidor  

  
1.  No computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , abra RGui.exe como administrador.  Se você tiver instalado o SQL Server R Services usando os padrões, RGui.exe poderá ser encontrado em C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64.  
  
    Ou, se você instalou outro ambiente do R no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como RStudio), será possível usar o console do R para executar os comandos.  
  
2.  Em um prompt do R, execute os seguintes comandos do R:  
  
    ```  
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])  
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    ```  
  
**Observações:**  
  
-   Este exemplo usa a função grep do R para pesquisar o vetor dos caminhos disponíveis e encontrar o mais adequado em “Arquivos de Programas”. Para obter mais informações, visite [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep).   
  
-   Se você acha que os pacotes já estão instalados, verifique a lista de pacotes instalados usando a função R, `installed.packages()`.  
  
-   No cliente, você pode instalar na biblioteca de um usuário, se não quiser gravar na biblioteca principal em Arquivos de Programas. No entanto, ao instalar pacotes no computador do SQL Server, você deverá instalá-los na biblioteca padrão usada pelos serviços de R do SQL Server. Não use uma biblioteca do usuário. Para saber mais, veja [Instalando novos pacotes de R no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).
      

## <a name="3-run-powershell-script-runsqlrwalkthroughps1"></a>3. Execute o script RunSQL_R_Walkthrough.ps1  

Você pode executar este script do PowerShell no computador em que a solução será criada, por exemplo, o computador no qual seu código do R será desenvolvido e testado. Esse computador deve poder se conectar ao computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o protocolo Pipes Nomeados.  
  
O script executa estas ações:  
  
-   Verifica se o SQL Native Client e os utilitários de linha de comando do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão instalados. A ferramenta de linha de comando é necessária para executar o [Utilitário bcp](../../tools/bcp-utility.md), que é usado para o carregamento em massa rápido de dados em tabelas SQL.    
-   Conecta-se à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa alguns scripts do [!INCLUDE[tsql](../../includes/tsql-md.md)] que configuram o banco de dados e criam as tabelas para o modelo e os dados.    
-   Executa um script SQL para criar vários procedimentos armazenados.    
-   Carrega os dados baixados anteriormente na tabela nyctaxi_sample.    
-   Grava os argumentos novamente no arquivo de script do R para usar o nome do banco de dados especificado. 

### <a name="to-run-the-script"></a>Para executar o script
  
1.  Abra uma linha de comando do PowerShell como administrador.    
  
2.  Procure a pasta em que você baixou os scripts e digite o nome do script, como mostrado abaixo. Pressione ENTER.  
  
    ```  
    .\RunSQL_R_Walkthrough.ps1  
    ```  
  
3.  Para cada um dos seguintes parâmetros, será solicitado o seguinte:  
  
    - O nome do banco de dados que você deseja criar. 
      Por exemplo, você pode digitar **Tutorial** ou **Táxi**  
    - Credenciais sob as quais executar o script. Há duas opções:
        + Digite o nome de um logon SQL que tem privilégios CREATE DATABASE, e forneça a senha do SQL em um prompt sucessivo.
        + Pressione ENTER sem digitar qualquer nome para usar sua própria identidade do Windows e, no prompt protegido, digite sua senha do Windows... O PowerShell não oferece suporte para a inserção de um nome de usuário diferente do Windows. 

          Se você não especificar um usuário válido, o script usará a autenticação integrada do Windows como padrão.  
  
    -   O caminho completo para o arquivo csv que você deseja carregar no banco de dados  
  
        O script deverá baixar o arquivo e carregar os dados no banco de dados automaticamente, mas se isso falhar, você poderá sempre carregar os dados manualmente.  
  
4.  Pressione ENTER para executar o script.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 
 Se você tiver problemas, será possível executar todos ou qualquer uma das etapas manualmente, usando as linhas do script do PowerShell como exemplos. 
 

### <a name="the-powershell-script-didnt-download-the-data"></a>O script do PowerShell não baixou os dados para você
  
Para baixar os dados manualmente, clique com o botão direito do mouse no link a seguir e selecione **Salvar destino como**.  
  
[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)  
  
Anote o caminho para o arquivo de dados baixado e o nome do arquivo em que os dados foram salvos. Você precisará do caminho para carregar os dados na tabela usando o **bcp**.  
  
### <a name="i-was-unable-to-download-the-data"></a>Não foi possível baixar os dados
O arquivo de dados é grande. Use um computador que tenha uma conexão de Internet relativamente boa ou o download pode expirar.  

  
### <a name="could-not-connect-or-script-failed"></a>Não foi possível conectar ou ocorreu falha no script  
  
+ Verifique a ortografia do nome da instância. 
+ Verifique a cadeia de conexão completa.    
+ Dependendo dos requisitos da rede, o nome da instância poderá exigir qualificação com um ou mais nomes de sub-rede.  Por exemplo, se MYSERVER não funcionar, tente myserver.subnet.mycompany.com.
  
### <a name="network-error-or-protocol-not-found"></a>Erro de rede ou o protocolo não foi encontrado  
  
+ Verifique se a instância dá suporte a conexões remotas.    
+ Verifique se o usuário especificado do SQL pode se conectar remotamente ao banco de dados e se o protocolo Pipes Nomeados está habilitado na instância.    
+ Verifique as permissões da conta. A conta especificada pode não ter as permissões para criar um novo banco de dados e carregar os dados.  

### <a name="bcp-did-not-run"></a>O bcp não foi executado  

+ Verifique se o [utilitário bcp](../../tools/bcp-utility.md) está disponível no computador. Você pode executar o bcp de uma janela do PowerShell ou de um prompt de comando do Windows.
+ Se você receber um erro, adicione o local do utilitário bcp à variável de ambiente do sistema PATH e tente novamente.  

### <a name="the-table-schema-was-created-but-there-is-no-data-in-the-table"></a>O esquema da tabela foi criado, mas não há nenhum dado na tabela

Se o restante do script foi executado sem problemas, você poderá carregar os dados na tabela manualmente, usando o **bcp** na linha de comando, da seguinte maneira:  


 
**Usando um logon do SQL**
    
~~~~ 
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password  
~~~~  
  
**Usando a autenticação do Windows**  

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T 
~~~~ 
  
  
+ A palavra-chave **in** especifica a direção da movimentação de dados.  
+ O argumento **-f** exige que você especifique o caminho completo de um arquivo de formato. Um arquivo de formato é necessário se você usar a opção **in**.
+ Use os argumentos **-U** e **-P** se estiver executando o bcp com um logon SQL.
+ Use o argumento **-T** se estiver usando a autenticação integrada do Windows. 

  
### <a name="how-can-i-run-the-script-without-prompts"></a>Como posso executar o script sem prompts?  
  
Você pode especificar todos os parâmetros em uma única linha de comando, usando valores específicos ao seu ambiente. 
  
```  
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>  
```  
  
Por exemplo, para executar o script usando um logon SQL:  
  
```  
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv  
```  
  
Este exemplo faz o seguinte:  
  
-   Conecta-se à instância especificada e ao banco de dados usando as credenciais de *SqlUserName*.  
-   Obtém os dados do arquivo *C:\temp\nyctaxi1pct.csv*.  
-   Carrega os dados para a tabela *dbo.nyctaxi_sample*, no banco de dados *MyDB* na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada *MyServer*.  

### <a name="the-data-loaded-but-it-contains-duplicates"></a>Os dados foram carregados, mas eles contêm duplicatas

Se já existir uma tabela e ela tiver o esquema correto, o bcp continuará sendo executado, mas inserirá uma nova cópia dos dados em vez de substituir os dados existentes. Isso resultará em dados duplicados.  Certifique-se de truncar as tabelas existentes antes de executar novamente o script.

## <a name="what-the-download-includes"></a>O que o download inclui

Ao baixar os arquivos do repositório GitHub, você obterá o seguinte:
+ Dados em formato CSV
+ Um script do PowerShell para preparar o ambiente
+ Um arquivo de formato XML para importar os dados para o SQL Server usando o bcp
+ Vários scripts T-SQL
+ Todo o código do R que você precisa para executar este passo a passo

### <a name="training-and-scoring-data"></a>Dados de pontuação e treinamento  
Os dados são uma amostragem representativa do conjunto de dados de táxi de Nova York, que contém registros de mais de 173 milhões de corridas individuais em 2013, incluindo tarifas e valores de gorjetas pagas por cada corrida.  Para obter mais informações sobre como esses dados foram originalmente coletados e como você pode obter o conjunto de dados completo, consulte  
[http://chriswhong.com/open-data/foil_nyc_taxi/](http://chriswhong.com/open-data/foil_nyc_taxi/).  
  
Para facilitar o trabalho com os dados, a equipe de ciência de dados da Microsoft reduziu a resolução para obter apenas 1% dos dados.  Esses dados foram compartilhados em um contêiner do armazenamento de blobs público no Azure, em formato .CSV. Os dados de origem são um arquivo não compactado, com quase 350 MB.  
 
### <a name="files"></a>Arquivos

 
+ **RunSQL_R_Walkthrough.ps1** Você executará esse script primeiro, usando o PowerShell. Ele chama os scripts SQL para carregar dados no banco de dados.  
    
+ **taxiimportfmt.xml** Um arquivo de definição de formato que é usado pelo utilitário BCP para carregar dados no banco de dados.
      
+ **RSQL_R_Walkthrough.R** Este é o script principal do R que será usado no restante das lições para fazer a análise e a modelagem de dados. Ele fornece todo o código do R de que você precisa para explorar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , criar o modelo de classificação e criar gráficos.   
  
### <a name="sql-scripts"></a>Scripts SQL  
Este script do PowerShell executa vários scripts do [!INCLUDE[tsql](../../includes/tsql-md.md)] no servidor. A tabela a seguir lista os arquivos de script do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Nome do arquivo de script SQL|O que ele faz|  
|------------------------|----------------|  
|create-db-tb-upload-data.sql|Cria o banco de dados e duas tabelas:<br /><br /> *nyctaxi_sample*: tabela que armazena os dados de treinamento, um exemplo de 1% do conjunto de dados de táxi de Nova York. Um índice columnstore clusterizado é adicionado à tabela para melhorar o desempenho de armazenamento e consulta.<br /><br /> *nyc_taxi_models*: uma tabela vazia que você usará posteriormente para salvar o modelo de classificação treinado.|  
|PredictTipBatchMode.sql|Cria um procedimento armazenado que chama um modelo treinado para prever os rótulos das novas observações. Aceita uma consulta como seu parâmetro de entrada.|  
|PredictTipSingleMode.sql|Cria um procedimento armazenado que chama um modelo de classificação treinado para prever os rótulos das novas observações. As variáveis das novas observações são passadas como parâmetros na linha.|  
|PersistModel.sql|Cria um procedimento armazenado que ajuda a armazenar a representação binária do modelo de classificação em uma tabela do banco de dados.|  
|fnCalculateDistance.sql|Cria uma função de valor escalar do SQL que calcula a distância direta entre os locais de embarque e desembarque de passageiros.|  
|fnEngineerFeatures.sql|Cria uma função com valor de tabela SQL que cria recursos para treinar o modelo de classificação|  
  
Todas as consultas SQL fornecidas como parte deste passo a passo foram testadas e podem ser usadas no estado em que se encontram no código do R. No entanto, se você quer realizar mais testes ou desenvolver sua própria solução usando consultas SQL, recomendamos o uso de um ambiente de desenvolvimento, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , para testar e ajustar as consultas primeiro, antes de adicioná-las ao código do R.  
  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 2: Exibir e explorar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lição anterior  
[Passo a passo de ponta a ponta sobre a ciência de dados](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
  
  
