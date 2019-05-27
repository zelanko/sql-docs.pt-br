---
title: Destino OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dc2b3a1f77c7d0f2f00c1a08f27c27887cc4b73f
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65802351"
---
# <a name="ole-db-destination"></a>Destino OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O destino OLE DB carrega os dados em uma variedade de bancos de dados compatíveis com OLE DB usando uma tabela ou exibição de banco de dados ou um comando SQL. Por exemplo, a fonte OLE DB pode carregar dados em tabelas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access e nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 O destino OLE DB fornece cinco modos diferentes de acesso para carregar dados:  
  
-   Uma tabela ou exibição. Você pode especificar uma tabela ou exibição existente ou criar uma tabela nova.  
  
-   Uma tabela ou exibição que usa opções de carregamento rápido. Você pode especificar uma tabela existente ou criar uma tabela nova.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Uma tabela ou exibição especificada em uma variável que usa opções de carregamento rápido.  
  
-   Os resultados de uma instrução SQL.  
  
> [!NOTE]  
>  O destino OLE DB não aceita parâmetros. Se você precisar executar uma instrução parametrizada INSERT, considere a transformação Comando OLE DB. Para obter mais informações, consulte [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 Quando o destino OLE DB carrega dados que usam o conjunto de caracteres de dois bytes (DBCS), os dados poderão ser corrompidos se o modo de acesso de dados não usar a opção de carregamento rápido e se o gerenciador de conexões OLE DB usar o provedor OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB). Para garantir a integridade dos dados DBCS, você deve configurar o gerenciador de conexões OLE DB para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ou utilizar um dos modos de acesso de carregamento rápido: **Tabela ou exibição – carregamento rápido** ou **Variável de nome da tabela ou exibição – carregamento rápido**. As duas opções estão disponíveis na caixa de diálogo **Editor de Destino de OLE DB** . Ao programar o modelo de objeto do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , você deve definir a propriedade AccessMode para **OpenRowset usando FastLoad**ou **OpenRowset usando FastLoad da Variável**.  
  
> [!NOTE]  
>  Se você usar a caixa de diálogo **Editor de Destino de OLE DB** no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer para criar a tabela de destino em que o destino OLE DB insere dados, você poderá ter que selecionar a nova tabela manualmente. A necessidade de selecionar manualmente ocorre quando um provedor OLE DB, como o provedor OLE DB para DB2, adiciona automaticamente identificadores de esquema ao nome da tabela.  
  
> [!NOTE]  
>  A instrução CREATE TABLE gerada pela caixa de diálogo **Editor de Destino de OLE DB** pode requerer modificação dependendo do tipo de destino. Por exemplo, alguns destinos não suportam os tipos de dados que a instrução CREATE TABLE usa.  
  
 Esse destino usa um gerenciador de conexões OLE DB para conectar-se a uma fonte de dados e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também fornece o objeto de fonte de dados do qual você pode criar um gerenciador de conexões OLE DB, disponibilizando as fontes de dados e exibições da fonte de dados para o destino OLE DB.  
  
 Um destino OLE DB inclui mapeamentos entre as colunas de entrada e as colunas da fonte de dados de destino. Você não precisa mapear as colunas de entrada para todas as colunas de destino, mas, dependendo das propriedades das colunas de destino, podem ocorrer erros se nenhuma das colunas de entrada for mapeada para as colunas de destino. Por exemplo, se uma coluna de destino não permitir valores nulos, uma coluna de entrada deve ser mapeada para aquela coluna de destino. Além disso, os tipos de dados de colunas mapeadas devem ser compatíveis. Por exemplo, você não pode mapear uma coluna de entrada que tenha um tipo de dados de cadeia de caracteres para uma coluna com um tipo de dados numérico.  
  
 O destino OLE DB tem uma entrada regular e uma saída de erro.  
  
 Para obter mais informações sobre tipos de dados, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="fast-load-options"></a>Opções de carregamento rápido  
 Se o destino OLE DB usa um modo de acesso a dados de carregamento rápido, você pode especificar as seguintes opções na interface do usuário, **Editor de Destino de OLE DB**, para esse destino:  
  
-   Manter os valores de identidade do arquivo de dados importado ou usar valores exclusivos atribuídos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Reter um valor nulo durante a operação de carregamento em massa.  
  
-   Verificar restrições na tabela ou exibição de destino durante a operação de importação em massa.  
  
-   Adquirir um bloqueio em nível de tabela pela duração da operação de carregamento em massa.  
  
-   Especificar o número de linhas no lote e o tamanho de confirmação.  
  
 Algumas opções de carregamento rápido são armazenadas em propriedades específicas do destino OLE DB. Por exemplo, FastLoadKeepIdentity especifica se os valores de identidade são mantidos ou não, FastLoadKeepNulls especifica se valores nulos são mantidos ou não e FastLoadMaxInsertCommitSize especifica o número de linhas a serem confirmadas como um lote. Outras opções de carregamento rápido são armazenadas em uma lista separada por vírgulas na propriedade FastLoadOptions. Se o destino OLE DB usa todas as opções de carregamento rápido que estão armazenadas em FastLoadOptions e listadas na caixa de diálogo **Editor de Destino de OLE DB** , o valor da propriedade é definido como **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**. O valor 1000 indica que o destino é configurado para usar lotes de 1000 linhas.  
  
> [!NOTE]  
>  Qualquer falha de restrição ao destino fará com que todo o lote de linhas definido por FastLoadMaxInsertCommitSize falhe.  
  
 Além das opções de carregamento rápido apresentadas na caixa de diálogo **Editor de Destino de OLE DB** , você pode configurar o destino OLE DB para usar as seguintes opções de carregamento em massa informando-as na propriedade FastLoadOptions na caixa de diálogo **Editor Avançado** .  
  
|Opção de carregamento rápido|Descrição|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Especifica o tamanho em quilobytes a ser inserido. Esta opção tem o formato **KILOBYTES_PER_BATCH** = \<valor inteiro positivo**>**.|  
|FIRE_TRIGGERS|Especifica se os gatilhos devem ser disparados na tabela de inserção. A opção tem o formato **FIRE_TRIGGERS**. A presença da opção indica que os gatilhos irão disparar.|  
|ORDER|Especifica como os dados de entrada são classificados. A opção tem o formato ORDER \<nome da coluna> ASC&#124;DESC. Qualquer número de colunas pode ser listado e a inclusão da ordem de classificação é opcional. Se a ordem de classificação for omitida, a operação de inserção assumirá que os dados não estão classificados.<br /><br /> Observação: o desempenho pode ser otimizado se você usar a opção ORDER para classificar os dados de entrada de acordo com o índice clusterizado da tabela.|  
  
 As palavras-chave [!INCLUDE[tsql](../../includes/tsql-md.md)] são normalmente digitadas em letras maiúsculas, mas não fazem distinção entre maiúsculas e minúsculas.  
  
 Para saber mais sobre opções de carregamento rápido, consulte [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="troubleshooting-the-ole-db-destination"></a>Solucionando problemas do destino OLE DB  
 Você pode registrar as chamadas que o destino OLE DB faz para provedores de dados externos. Você pode usar esse recurso de registro para solucionar problemas ao salvar os dados em fontes de dados externas que o destino OLE DB executa. Para registrar as chamadas que o destino OLE DB faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-destination"></a>Configurando o destino OLE DB  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Carregar dados por meio do destino OLE DB](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>Editor de Destino OLE DB (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de OLE DB** para selecionar a conexão OLE DB para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** do destino OLE DB não está disponível no **Editor de Destino OLE DB**, mas pode ser definida usando o **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Destino OLE DB em [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Modo de acesso aos dados**  
 Especifique o método de carregamento de dados no destino. O carregamento de conjunto de caracteres de bytes duplos (DBCS) requer o uso de uma das opções de carregamento rápido. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma tabela ou exibição no destino OLE DB.|  
|Tabela ou exibição - carregamento rápido|Carregue dados em uma tabela ou exibição no destino OLE DB e use a opção de carregamento rápido. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Nome da tabela ou variável do nome de exibição|Especifique a tabela ou nome de exibição em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Variável do nome da tabela ou do nome de exibição - carregamento rápido|Especifique o nome da tabela ou exibição em uma variável e use a opção de carregamento rápido para carregar dados. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Comando SQL|Carregue dados no destino OLE DB usando uma consulta SQL.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
 Cada uma das configurações do **Modo de acesso aos dados** exibe um conjunto de opções dinâmicas específico àquela configuração. As seções a seguir descrevem todas as opções dinâmicas disponíveis de cada configuração de **Modo de acesso aos dados** .  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
#### <a name="data-access-mode--table-or-view---fast-load"></a>Modo de acesso a dados = tabela ou exibição – carregamento rápido  
 **Nome da tabela ou exibição**  
 Selecione uma tabela ou exibição do banco de dados nessa lista ou crie uma nova tabela clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Manter identidade**  
 Especifique se os valores de identidade serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **false**.  
  
 **Manter nulos**  
 Especifique se os valores nulos serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **false**.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela será bloqueada durante o carregamento. O valor padrão dessa propriedade é **true**.  
  
 **Verificar restrições**  
 Especifique se o destino verificará as restrições quando os dados forem carregados. O valor padrão dessa propriedade é **true**.  
  
 **Linhas por lote**  
 Especifique o número de linhas em um lote. O valor padrão dessa propriedade é **-1**, que indica que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino de OLE DB** para indicar que você não deseja atribuir um valor personalizado para essa propriedade.  
  
 **Tamanho máximo de confirmação de inserção**  
 Especifique o tamanho do lote que o destino OLE DB tenta confirmar durante as operações de carregamento rápido. O valor **0** indica que todos os dados serão confirmados em um único lote depois que todas as linhas forem processadas.  
  
> [!NOTE]  
>  O valor **0** pode fazer com que o pacote em execução deixe de responder se o destino OLE DB e outro componente de fluxo de dados estiverem atualizando a mesma tabela de origem. Para impedir que o pacote pare, defina a opção **Tamanho máximo de confirmação de inserção** como **2147483647**.  
  
 Se você fornecer um valor para essa propriedade, o destino confirmará as linhas nos lotes que forem menores que (a) o **Tamanho máximo de confirmação de inserção**ou (b) as linhas restantes no buffer que estiverem sendo processadas no momento.  
  
> [!NOTE]  
>  Qualquer falha de restrição ao destino fará com que todo o lote de linhas definido pelo **Tamanho máximo de confirmação de inserção** falhe.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>Modo de acesso a dados = Variável do nome da tabela ou do nome de exibição – carregamento rápido)  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Manter identidade**  
 Especifique se os valores de identidade serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **false**.  
  
 **Manter nulos**  
 Especifique se os valores nulos serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **false**.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela será bloqueada durante o carregamento. O valor padrão dessa propriedade é **false**.  
  
 **Verificar restrições**  
 Especifique se a tarefa verificará as restrições. O valor padrão dessa propriedade é **false**.  
  
 **Linhas por lote**  
 Especifique o número de linhas em um lote. O valor padrão dessa propriedade é **-1**, que indica que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino de OLE DB** para indicar que você não deseja atribuir um valor personalizado para essa propriedade.  
  
 **Tamanho máximo de confirmação de inserção**  
 Especifique o tamanho do lote que o destino OLE DB tenta confirmar durante as operações de carregamento rápido. O valor padrão **2147483647** indica que todos os dados serão confirmados em um único lote depois que todas as linhas forem processadas.  
  
> [!NOTE]  
>  O valor **0** pode fazer com que o pacote em execução deixe de responder se o destino OLE DB e outro componente de fluxo de dados estiverem atualizando a mesma tabela de origem. Para impedir que o pacote pare, defina a opção **Tamanho máximo de confirmação de inserção** como **2147483647**.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
> [!NOTE]  
>  O destino OLE DB não aceita parâmetros. Se você precisar executar uma instrução parametrizada INSERT, considere a transformação Comando OLE DB. Para obter mais informações, consulte [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 **Construir consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="ole-db-destination-editor-mappings-page"></a>Editor de Destino de OLE DB (página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo **Editor de Destino de OLE DB** para mapear colunas de entrada para colunas de destino.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear colunas de entrada disponíveis na tabela para as colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis na tabela para as colunas de entrada.  
  
 **Coluna de Entrada**  
 Exiba as colunas de entrada que você selecionou. Você pode remover mapeamentos selecionando **\<ignorar>** para excluir colunas da saída.  
  
 **Coluna de Destino**  
 Visualize cada coluna de destino disponível, esteja ela mapeada ou não.  
  
## <a name="ole-db-destination-editor-error-output-page"></a>Editor de Destino de OLE DB (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Destino OLE DB** para especificar opções de tratamento de erros.  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Visualize o nome da entrada.  
  
 **Coluna**  
 Não usado.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos relacionados:** [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Não usado.  
  
 **Descrição**  
 Visualize a descrição da operação.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Origem de OLE DB](../../integration-services/data-flow/ole-db-source.md)  
  
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
