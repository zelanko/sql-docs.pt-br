---
title: Carregar com o Integration Services
description: Fornece informações de referência e implantação para carregar dados em Parallel data warehouse (PDW) usando pacotes do SQL Server Integration Services (SSIS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b0bcb5cfe1ec4111aaea7153f35bca084df62b76
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401010"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Carregar dados com Integration Services em paralelo data warehouse
Fornece informações de referência e implantação para carregar dados em SQL Server paralelo data warehouse usando pacotes do SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Algumas  
Integration Services é o componente de SQL Server para extração, transformação e carregamento (ETL) de alto desempenho, e normalmente é usado para popular e atualizar uma data warehouse.  
  
O adaptador de destino do PDW é um componente Integration Services que permite carregar dados no PDW usando Integration Services pacotes dtsx. Em um fluxo de trabalho de pacote para SQL ServerPDW, você pode carregar e mesclar dados de várias fontes e carregar dados em vários destinos. As cargas ocorrem em paralelo, ambas dentro de um pacote e entre vários pacotes em execução simultânea, até um máximo de 10 cargas em execução em paralelo na mesma aplicação.  
  
Além das tarefas descritas neste tópico, você pode usar outros recursos do Integration Services para filtrar, transformar, analisar e limpar seus dados antes de carregá-los no data warehouse. Você também pode aprimorar o fluxo de trabalho do pacote por meio da execução de instruções SQL, execução de pacotes filho ou envio de email.  
  
Para obter a documentação completa do Integration Services, consulte [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).  
  
## <a name="HowToDeployPackage"></a>Métodos para executar um pacote de Integration Services  
Use um desses métodos para executar um pacote de Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Executar de SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Para executar o pacote de dentro do BIDS, clique com o botão direito do mouse no pacote e escolha **executar pacote**.  
  
Por padrão, o BIDS executa pacotes usando binários de 64 bits. Isso é determinado pela propriedade do pacote **Run64BitRuntime** . Para definir essa propriedade, vá para **Gerenciador de soluções**, clique com o botão direito do mouse em seu projeto e escolha **Propriedades**. Nas **páginas de propriedades do Integration Services**, vá para propriedades de **configuração** e selecione **depuração**. Você verá a propriedade **Run64BitRuntime** nas opções de **depuração**. Para usar tempos de execução de 32 bits, defina como **false**. Para usar tempos de execução de 64 bits, defina como **true**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Executar do SQL Server 2012 SQL Server Data Tools  
Para executar o pacote de dentro do SQL Server Data Tools, clique com o botão direito do mouse no pacote e escolha **executar pacote**.  
  
### <a name="run-from-powershell"></a>Executar do PowerShell  
Para executar o pacote do Windows PowerShell, usando o utilitário **dtexec** :`dtexec /FILE <packagePath>`  
  
Por exemplo, `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Executar a partir de um prompt de comando do Windows 
Para executar o pacote de um prompt de comando do Windows, usando o utilitário **dtexec** :`dtexec /FILE <packagePath>`  
  
Por exemplo: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Tipos de dados  
Ao usar o Integration Services para carregar dados de uma fonte de dados para um SQL Server PDW, os dados são mapeados primeiro a partir dos dados de origem para Integration Services tipos de dados. Isso permite que dados de várias fontes de dados sejam mapeados para um conjunto comum de tipos de dados.  
  
Em seguida, os dados são mapeados de Integration Services para SQL Server PDW tipos de dados. Para cada tipo de dados SQL Server PDW, a tabela a seguir lista os tipos de dados de Integration Services que podem ser convertidos para o tipo de dados SQL Server PDW.  
  
|Tipo de dados do PDW|Integration Services tipos de dados que são mapeados para o tipo de dados do PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|BIGINT|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
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
  
O PDW gera um erro de validação se você mapear uma DT_NUMERIC ou DT_DECIMAL coluna de entrada que contenha um valor com precisão maior que 28.  
  
**Tipos de dados sem suporte**  
  
SQL Server PDW não oferece suporte aos seguintes tipos de dados de Integration Services:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Para carregar colunas que contêm dados desses tipos em SQL Server PDW, você deve adicionar uma transformação conversão de dados upstream no fluxo de dados para converter os dados em um tipo de dados compatível.  
  
## <a name="permissions"></a>Permissões  
Para executar um pacote de carga de Integration Services, você precisa:  
  
-   Permissão de carregamento no banco de dados.  
  
-   Permissões de inserção, atualização e exclusão aplicáveis na tabela de destino.  
  
-   Se um banco de dados de preparo for usado, crie a permissão no banco de dados de preparo. Isso é para a criação de uma tabela temporária.  
  
-   Se nenhum banco de dados de preparo for usado, a permissão CREATE no banco de dados de destino. Isso é para a criação de uma tabela temporária.  
  
## <a name="GenRemarks"></a>Comentários gerais  
Quando um pacote de Integration Services tem vários destinos de SQL Server PDW em execução e uma das conexões é encerrada, Integration Services para enviar dados por push para todos os destinos de SQL Server PDW.  
  
## <a name="Limits"></a>Limitações e restrições  
Para um pacote de Integration Services, o número de destinos de SQL Server PDW para a mesma fonte de dados é limitado pelo número máximo de cargas ativas. O número máximo é pré-configurado e não pode ser configurado pelo usuário. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Cada destino do pacote de Integration Services para a mesma fonte de dados conta como uma carga quando o pacote está em execução. Por exemplo, suponha que o número máximo de cargas ativas é 10. O pacote não será executado ao tentar abrir 11 ou mais destinos para a mesma fonte de dados.  
  
Vários pacotes podem ser executados simultaneamente desde que cada pacote não use mais do que o número máximo de cargas ativas. Por exemplo, se o número máximo de cargas ativas for 10, você poderá executar simultaneamente dois pacotes que usem 10 destinos cada um. Um pacote será executado enquanto o outro esperar na fila de carga.  
  
Se o número de cargas na fila de carga exceder o número máximo de cargas em fila, o pacote não será executado. Por exemplo, se o número máximo de cargas for 10 por dispositivo e o número máximo de cargas enfileiradas for 40 por dispositivo, você poderá executar simultaneamente cinco pacotes de Integration Services que cada um dos 10 destinos abertos. Se você tentar executar um sexto pacote, ele não será executado.  

> [!IMPORTANT]
> Usar uma OLE DB fonte de dados no SSIS com o adaptador de destino do PDW pode causar corrupção de dados se a tabela de origem contiver colunas char e varchar com agrupamentos do SQL. É recomendável usar uma origem ADO.NET se a tabela de origem contiver colunas char ou varchar com agrupamentos SQL. 

  
## <a name="Locks"></a>Comportamento de bloqueio  
Ao carregar dados com Integration Services, o SQL ServerPDW usa bloqueios em nível de linha para atualizar dados na tabela de destino. Isso significa que cada linha é bloqueada para leitura e gravação enquanto está sendo atualizada. As linhas da tabela de destino não são bloqueadas enquanto os dados são carregados na tabela de preparo.  
  
## <a name="Examples"></a>Disso  
  
### <a name="Walkthrough"></a>Um. Carga simples de arquivo simples  
A instrução a seguir demonstra uma simples carga de dados usando Integration Services para carregar dados de arquivo simples para um dispositivo SQL Server PDW.  Este exemplo supõe que o Integration Services já foi instalado no computador cliente e o destino SQL Server PDW foi instalado, conforme descrito acima.  
  
Neste exemplo, vamos carregar na `Orders` tabela, que tem a seguinte DDL. A `Orders` tabela faz parte do `LoadExampleDB` banco de dados.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
Estes são os dados de carga:  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
Em preparação para a carga, crie o arquivo `exampleLoad.txt`simples, contendo os dados de carga:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
Primeiro, crie um pacote de Integration Services executando estas etapas:  
  
1.  Em SQL Server Data Tools \(SSDT\), selecione **arquivo**, **novo**e **projeto**. Selecione **Integration Services projeto** nas opções listadas. Nomeie este projeto `ExampleLoad`e clique em **OK**.  
  
2.  Clique na guia **fluxo de controle** e arraste a **tarefa fluxo de dados** da **caixa de ferramentas** para o painel fluxo de **controle** .  
  
3.  Clique na guia **fluxo de dados** e arraste **fonte de arquivo simples** da **caixa de ferramentas** para o painel fluxo de **dados** . Clique duas vezes na caixa que você acabou de criar para abrir o **Editor de fonte de arquivo simples**.  
  
4.  Clique em **Gerenciador de conexões** e em **novo**.  
  
5.  Na caixa **nome do Gerenciador de conexões** , insira um nome amigável para a conexão. Para este exemplo, `Example Load Flat File CM`.  
  
6.  Clique em **procurar** e selecione `ExampleLoad.txt` o arquivo no computador local.  
  
7.  Como o arquivo simples contém uma linha com nomes de coluna, clique nos **nomes de coluna na primeira caixa de linha de dados** .  
  
8.  Clique em **colunas** na coluna esquerda e visualize os dados que serão carregados para certificar-se de que os nomes de coluna e os dados foram interpretados corretamente.  
  
9. Clique em **avançado** na coluna esquerda. Clique em cada nome de coluna para examinar o tipo de dados que foi associado aos dados. Digite as alterações na caixa para que os tipos de dados dos dados carregados sejam compatíveis com os tipos de coluna de destino.  
  
10. Clique em **OK** para salvar o Gerenciador de conexões.  
  
11. Clique em **OK** para sair do **Editor de fonte de arquivo simples**.  
  
Especifique o destino para o fluxo de dados.  
  
1.  Arraste o **destino SQL Server PDW** da **caixa de ferramentas** para o painel **fluxo de dados** .  
  
2.  Clique duas vezes na caixa que você acabou de criar para carregar o **Editor de destino SQL Server PDW**.  
  
3.  Clique na seta para baixo ao lado do **Gerenciador de conexões**.  
  
4.  Selecione **criar uma nova conexão**.  
  
5.  Preencha as informações do servidor, do usuário, da senha e do banco de dados de destino com informações específicas para seu dispositivo. (Exemplos são mostrados abaixo). Em seguida, clique em **OK**.  
  
    Para conexões InfiniBand, **nome do servidor**: Insira <nome do dispositivo>-SQLCTL01, 17001.  
  
    Para conexões Ethernet, **nome do servidor**: Insira o endereço IP do cluster do nó de controle, a vírgula, a porta 17001. Por exemplo, 10.192.63.134, 17001.  
  
    **Usuário**`user1`  
  
    **La**`password1`  
  
    **Banco de dados de destino:**`LoadExampleDB`  
  
6.  Selecione a tabela de destino `Orders`:.  
  
7.  Selecione **acrescentar** como o modo de carregamento e clique em **OK**.  
  
Especifique o fluxo de dados da origem para o destino.  
  
1.  No painel **fluxo de dados** , arraste a seta verde da caixa **fonte de arquivo simples** para a caixa **SQL Server PDW destino** .  
  
2.  Clique duas vezes na caixa **SQL Server PDW destino** para que você veja o **Editor de destino SQL Server PDW** novamente. Você deve ver os nomes de coluna do arquivo simples à esquerda, em **colunas de entrada não mapeadas**. Você deve ver os nomes de coluna da tabela de destino à direita, em **colunas de destino não mapeadas**. Mapeie as colunas arrastando ou clicando duas vezes nos nomes de coluna correspondentes nas listas colunas de **entrada não mapeadas** e **colunas de destino não mapeadas** para a caixa **colunas mapeadas** . Clique em **OK** para salvar as configurações.  
  
3.  Salve o pacote clicando em **salvar** no menu **arquivo** .  
  
Execute o pacote no seu computador Integration Services.  
  
1.  Na**Gerenciador de Soluções** Integration Services (coluna direita), clique `Package.dtsx` com o botão direito do mouse e selecione **executar**.  
  
2.  O pacote será executado e o progresso mais quaisquer erros serão mostrados no painel **progresso** . Use um cliente SQL para confirmar a carga ou monitore a carga por meio do console do administrador do SQL Server PDW.  
  
## <a name="see-also"></a>Consulte Também  
[Criar uma tarefa de script que usa o adaptador de destino do SSIS PDW](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[Projetando e implementando pacotes (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Tutorial: Criando um pacote básico usando um assistente](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Introdução (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[Exemplo de geração de pacote dinâmico](https://go.microsoft.com/fwlink/?LinkId=202413)  
[Projetando seus pacotes SSIS para o paralelismo (vídeo do SQL Server)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Exemplos da comunidade Microsoft SQL Server: Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[Melhorando cargas incrementais com o Change Data Capture](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[Transformação Dimensão de alteração lenta](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[Tarefa Inserção em Massa](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
