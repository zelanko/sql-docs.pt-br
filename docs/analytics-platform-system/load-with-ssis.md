---
title: Carregar dados com o Integration Services
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Fornece informações de referência e de implantação para carregar dados no SQL Server Parallel Data Warehouse usando pacotes do SQL Server Integration Services (SSIS).
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 9bdb559a-a91c-4342-8a6e-438cb93f975c
caps.latest.revision: 69
ms.openlocfilehash: d32e6b97d036437f6a28b81622873d14854d304f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="load-data-with-integration-services"></a>Carregar dados com o Integration Services
Fornece informações de referência e de implantação para carregar dados no SQL Server Parallel Data Warehouse usando pacotes do SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](http://msdn.microsoft.com/library/ms141091&#40;v=sql11&#40;.aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Noções básicas  
Serviços de integração é o componente do SQL Server de alto desempenho extração, transformação e carregamento (ETL) de dados e normalmente é usado para popular e atualizar um data warehouse.  
  
O adaptador de destino do PDW é um componente de serviços de integração que permite carregar dados em PDW usando pacotes dtsx do Integration Services. Em um fluxo de trabalho do pacote para ServerPDW SQL, você pode carregar e mesclar dados de várias origens e carregar dados para vários destinos. As cargas ocorrem em paralelo, ambas dentro de um pacote e entre vários pacotes em execução simultânea, até um máximo de 10 cargas em execução em paralelo na mesma aplicação.  
  
Além das tarefas descritas neste tópico, você pode usar outros recursos do Integration Services para filtrar, transformar, analisar e limpar seus dados antes de carregá-los no data warehouse. Você também pode aprimorar o fluxo de trabalho do pacote por meio da execução de instruções SQL, execução de pacotes filho ou envio de email.  
  
Para obter a documentação completa do Integration Services, consulte [SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026(v=sql11).aspx).  
  
## <a name="HowToDeployPackage"></a>Métodos para executar um pacote do Integration Services  
Use um destes métodos para executar um pacote do Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Execução do SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Para executar o pacote a partir BIDS, com o botão direito em seu pacote e escolha **executar pacote**.  
  
Por padrão, o BIDS executa pacotes usando os binários de 64 bits. Isso é determinado pelo **Run64BitRuntime** propriedade do pacote. Para definir essa propriedade, vá para **Solution Explorer**, com o botão direito no projeto e escolha **propriedades**. Sobre o **páginas de propriedades do Integration Services**, vá para **propriedades de configuração** e selecione **depuração**. Você verá o **Run64BitRuntime** propriedade sob o **opções de depuração**. Para usar tempos de execução de 32 bits, defina isso **False**. Para usar tempos de execução de 64 bits, defina isso **True**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Executar as ferramentas de dados do SQL Server 2012 SQL Server  
Para executar o pacote a partir do SQL Server Data Tools, clique com botão direito em seu pacote e escolha **executar pacote**.  
  
### <a name="run-from-powershell"></a>Execução do PowerShell  
Para executar o pacote do Windows PowerShell, usando o **dtexec** utilitário: `dtexec /FILE <packagePath>`  
  
Por exemplo, `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Prompt de comando executado de um Windows 
Para executar o pacote em um prompt de comando do Windows, usando o **dtexec** utilitário: `dtexec /FILE <packagePath>`  
  
Por exemplo: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Tipos de dados  
Ao usar o Integration Services para carregar dados de uma fonte de dados para um banco de dados do SQL Server PDW, os dados são mapeados primeiro dos dados de origem para tipos de dados do Integration Services. Isso permite que dados de várias fontes de dados sejam mapeados para um conjunto comum de tipos de dados.  
  
Em seguida, os dados são mapeados do Integration Services para tipos de dados do SQL Server PDW. Para cada tipo de dados do SQL Server PDW, a tabela a seguir lista os tipos de dados do Integration Services que podem ser convertidos para o tipo de dados do SQL Server PDW.  
  
|Tipo de dados do PDW|Tipos de dados Integration Services (s) que são mapeados para o tipo de dados do PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|FLOAT|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|REAL|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**Suporte limitado para precisão de tipo de dados**  
  
PDW gera um erro de validação se você mapear uma coluna de entrada DT_NUMERIC ou DT_DECIMAL que contém um valor com precisão maior que 28.  
  
**Tipos de dados sem suporte**  
  
SQL Server PDW não dá suporte para os seguintes tipos de dados do Integration Services:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Para carregar colunas que contêm dados desses tipos para o SQL Server PDW, você deve adicionar uma transformação de conversão de dados upstream no fluxo de dados para converter os dados para um tipo de dados compatível.  
  
## <a name="permissions"></a>Permissões  
Para executar um pacote de carga do Integration Services, você precisa:  
  
-   Permissão de carga no banco de dados.  
  
-   Aplicável INSERT, UPDATE, permissões de exclusão na tabela de destino.  
  
-   Se um banco de dados de preparo for usado, a permissão Criar o banco de dados de preparo. Isso é para criar uma tabela temporária.  
  
-   Se nenhum banco de dados de preparo for usado, permissão de criação do banco de dados de destino. Isso é para criar uma tabela temporária.  
  
## <a name="GenRemarks"></a>Comentários gerais  
Quando um pacote do Integration Services tem vários destinos de PDW do SQL Server em execução e uma das conexões é encerrada, o Integration Services para enviar dados por push para todos os destinos do SQL Server PDW.  
  
## <a name="Limits"></a>Limitações e restrições  
Para um pacote do Integration Services, o número de destinos do PDW do SQL Server para a mesma fonte de dados é limitado pelo número máximo de cargas ativas. O número máximo é pré-configurado e não pode ser configurado pelo usuário. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Cada destino de pacote do Integration Services para a mesma fonte de dados é contado como uma carga quando o pacote está em execução. Por exemplo, suponha que o número máximo de cargas ativas é 10. O pacote não será executado ao tentar abrir 11 ou mais destinos para a mesma fonte de dados.  
  
Vários pacotes podem ser executados simultaneamente desde que cada pacote não use mais do que o número máximo de cargas ativas. Por exemplo, se o número máximo de cargas ativas for 10, você poderá executar simultaneamente dois pacotes que usem 10 destinos cada um. Um pacote será executado enquanto o outro esperar na fila de carga.  
  
Se o número de cargas na fila de carga exceder o número máximo de cargas em fila, o pacote não será executado. Por exemplo, se o número máximo de cargas for 10 por aplicação, e o número máximo de cargas em fila for 40 por aplicação, você pode executar simultaneamente cinco pacotes do Integration Services que abrem 10 destinos cada. Se você tentar executar um sexto pacote, ele não será executado.  

> [!IMPORTANT]
> Usando uma fonte de dados OLE DB no SSIS com o adaptador de destino do PDW, pode causar corrupção de dados se a tabela de origem contém colunas char e varchar com agrupamentos do SQL. É recomendável usar uma origem ADO.NET se a tabela de origem contém colunas char ou varchar com agrupamentos do SQL. 

  
## <a name="Locks"></a>Comportamento de bloqueio  
Ao carregar os dados com o Integration Services, SQL ServerPDW usa bloqueios em nível de linha para atualizar dados na tabela de destino. Isso significa que cada linha é bloqueada para leitura e gravação enquanto está sendo atualizada. As linhas da tabela de destino não são bloqueadas enquanto os dados são carregados na tabela de preparo.  
  
## <a name="Examples"></a>Exemplos  
  
### <a name="Walkthrough"></a>A. Carga Simple de arquivo simples  
A instrução a seguir demonstra um carregamento de dados simples usando o Integration Services para carregar dados de arquivo simples em um dispositivo de PDW do SQL Server.  Este exemplo presume que o Integration Services já foi instalado no computador cliente e o destino do SQL Server PDW tiver sido instalado, conforme descrito acima.  
  
Neste exemplo, será carregado para o `Orders` tabela, que tem o DDL a seguir. O `Orders` tabela faz parte do `LoadExampleDB` banco de dados.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
Aqui está os carregar dados:  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
Em preparação para a carga, crie o arquivo simples `exampleLoad.txt`, que contém os dados de carga:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
Primeiro, crie um pacote do Integration Services, executando essas etapas:  
  
1.  No SQL Server Data Tools \(SSDT\), selecione **arquivo**, **novo**e, em seguida, **projeto**. Selecione **projeto do Integration Services** entre as opções listadas. Nomeie esse projeto `ExampleLoad`e clique em **Okey**.  
  
2.  Clique o **fluxo de controle** guia e, em seguida, arraste o **a tarefa de fluxo de dados** do **caixa de ferramentas** para o **fluxo de controle** painel.  
  
3.  Clique o **de fluxo de dados** guia e, em seguida, arraste **fonte de arquivo simples** do **caixa de ferramentas** para o **de fluxo de dados** painel. Clique duas vezes em caixa que você acabou de criar para abrir o **Editor de origem de arquivo simples**.  
  
4.  Clique em **Gerenciador de Conexão** e, em seguida, clique em **novo**.  
  
5.  No **nome do Gerenciador de Conexão** , digite um nome amigável para a conexão. Neste exemplo, `Example Load Flat File CM`.  
  
6.  Clique em **procurar** e selecione o `ExampleLoad.txt` arquivo do computador local.  
  
7.  Como o arquivo simples contém uma linha com nomes de coluna, clique no **nomes de coluna na primeira linha de dados** caixa.  
  
8.  Clique em **colunas** na coluna esquerda e visualizar os dados que serão carregados para verificar se os nomes de coluna e os dados foram interpretados corretamente.  
  
9. Clique em **avançado** na coluna esquerda. Clique em cada nome de coluna para analisar o tipo de dados que foi associado os dados. Digite as alterações na caixa de forma que os tipos de dados dos dados carregados serão compatíveis com os tipos de coluna de destino.  
  
10. Clique em **Okey** para salvar o Gerenciador de conexão.  
  
11. Clique em **Okey** para sair do **Editor de origem de arquivo simples**.  
  
Especifique o destino do fluxo de dados.  
  
1.  Arraste o **destino do SQL Server PDW** do **caixa de ferramentas** para o **de fluxo de dados** painel.  
  
2.  Clique duas vezes em caixa que você acabou de criar para carregar o **Editor de destino do SQL Server PDW**.  
  
3.  Clique na seta para baixo ao lado **Gerenciador de Conexão**.  
  
4.  Selecione **criar uma nova Conexão**.  
  
5.  Preencha as informações do banco de dados do servidor, usuário, senha e destino com informações específicas para seu dispositivo. (Os exemplos são mostrados abaixo). Em seguida, clique em **OK**.  
  
    Para conexões do InfiniBand, **nome do servidor**: insira o < nome do dispositivo >-SQLCTL01, 17001.  
  
    Para conexões Ethernet, **nome do servidor**: insira o endereço IP do cluster de nó de controle, vírgulas, porta 17001. Por exemplo, 10.192.63.134,17001.  
  
    **Usuário:**`user1`  
  
    **Senha:**`password1`  
  
    **Banco de dados de destino:**`LoadExampleDB`  
  
6.  Selecione a tabela de destino: `Orders`.  
  
7.  Selecione **Append** como o modo de carregamento e clique em **Okey**.  
  
Especifique o fluxo de dados de origem para destino.  
  
1.  No **de fluxo de dados** painel, arraste a seta verde do **fonte de arquivo simples** caixa para o **destino do SQL Server PDW** caixa.  
  
2.  Clique duas vezes o **destino do SQL Server PDW** caixa para que você veja o **Editor de destino do SQL Server PDW** novamente. Você deve ver os nomes de coluna do arquivo simples na esquerda, em **colunas de entrada não mapeadas**. Você deve ver os nomes de coluna da tabela de destino à direita, em **colunas de destino não mapeadas**. Mapear as colunas arrastando ou clicando duas vezes em nomes de coluna correspondente no **colunas de entrada não mapeadas** e **colunas de destino não mapeadas** lista para o **colunas mapeadas**caixa. Clique em **Okey** para salvar suas configurações.  
  
3.  Salve o pacote clicando em **salvar** no **arquivo** menu.  
  
Execute o pacote no computador do Integration Services.  
  
1.  No Integration Services**Solution Explorer** (coluna direita), clique com botão direito `Package.dtsx` e selecione **Execute**.  
  
2.  O pacote será executado e o andamento, bem como quaisquer erros serão mostrados no **andamento** painel. Use um cliente SQL para confirmar a carga ou monitorar a carga por meio do Console de administração do SQL Server PDW.  
  
## <a name="see-also"></a>Consulte também  
[Criar uma tarefa de script que usa o adaptador de destino do SSIS PDW](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026&#40;v=sql11&#40;.aspx)  
[Projetando e implementando pacotes (Integration Services)](http://msdn.microsoft.com/library/ms141091&#40;v=sql11&#40;.aspx)  
[Tutorial: Criando um pacote básico usando um assistente](http://technet.microsoft.com/library/ms365330&#40;v=sql11&#40;.aspx)  
[Guia de Introdução (Integration Services)](http://go.microsoft.com/fwlink/?LinkId=202412)  
[Exemplo de geração de pacote dinâmico](http://go.microsoft.com/fwlink/?LinkId=202413)  
[Projetando seus pacotes SSIS para o paralelismo (vídeo do SQL Server)](http://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server Community exemplos: Serviços de integração](http://go.microsoft.com/fwlink/?LinkId=202415)  
[Melhorando cargas incrementais com o Change Data Capture](http://msdn.microsoft.com/library/bb895315&#40;v=sql11&#40;.aspx)  
[Transformação Dimensão de Alteração Lenta](http://msdn.microsoft.com/library/ms141715&#40;v=sql11&#40;.aspx)  
[Tarefa Inserção em Massa](http://msdn.microsoft.com/library/ms141239&#40;v=sql11&#40;.aspx)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
