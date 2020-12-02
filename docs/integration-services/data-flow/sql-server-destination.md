---
description: destino do SQL Server
title: Destino do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlserverdest.f1
- sql13.dts.designer.sqlserverdestadapter.connection.f1
- sql13.dts.designer.sqlserverdestadapter.mappings.f1
- sql13.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2e7bc60bcfd7578d70528d92ef025370c28134e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194718"
---
# <a name="sql-server-destination"></a>destino do SQL Server

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O destino do SQL Server conecta-se a um banco de dados local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e efetua carregamentos de dados em massa em tabelas e modos de exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não é possível usar o destino do SQL Server em pacotes que acessam um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor remoto. Em vez disso, os pacotes devem usar o destino OLE DB. Para obter mais informações, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="permissions"></a>Permissões  
 Usuários que executam pacotes que incluem o destino do SQL Server precisam da permissão "Criar objetos globais". Você pode conceder esta permissão aos usuários usando a ferramenta Política de Segurança Local, aberta no menu **Ferramentas Administrativas** . Se você receber uma mensagem de erro ao executar um pacote que usa o destino do SQL Server, assegure-se de que a conta que executa o pacote tenha a permissão "Criar objetos globais".  
  
## <a name="bulk-inserts"></a>Inserções em massa  
 Se tentar usar o destino do SQL Server para carregar dados em massa em um banco de dados de um SQL Server remoto, você poderá ver uma mensagem de erro semelhante à seguinte: "Um registro OLE DB está disponível. Fonte: "Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 Descrição: “Não foi possível fazer o carregamento em massa porque o objeto de mapeamento de arquivo SSIS 'Global\DTSQLIMPORT ' não pôde ser aberto. Erro de sistema operacional código 2 (O sistema não pode achar o arquivo especificado.). Certifique-se de estar acessando um servidor local via "segurança do Windows."  
  
 O destino do SQL Server oferece a mesma inserção de dados em alta velocidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que a tarefa de Inserção em Massa fornece, porém, usando o destino do SQL Server, você pode aplicar transformações em dados de coluna antes de os dados serem carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para carregar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deve-se considerar o uso do destino do SQL Server em vez do destino do OLE DB.  
  
### <a name="bulk-insert-options"></a>Opções de inserção de massa  
 Se o destino do SQL Server usar um modo de acesso de dados da carga-rápida, você poderá especificar as seguintes opções de carga rápida:  
  
-   Reter valores de identidade do arquivo de dados importado ou usar valores exclusivos atribuídos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Reter valores nulos durante a operação de carregamento em massa.  
  
-   Verificar restrições na tabela de destino ou exibir durante a operação de importação em massa.  
  
-   Adquirir um bloqueio em nível de tabela pela duração da operação de carregamento em massa.  
  
-   Executar disparadores de inserção definidos na tabela de destino durante a operação de carregamento em massa.  
  
-   Especificar o número da primeira linha na entrada a ser carregada durante a operação de inserção em massa.  
  
-   Especificar o número da última linha na entrada a ser carregada durante a operação de inserção em massa.  
  
-   Especificar o número máximo de erros permitidos antes que a operação de inserção em massa seja cancelada. Cada linha que não puder ser importada será contada como um erro.  
  
-   Especificar as colunas na entrada que contêm dados ordenados.  
  
 Para obter mais informações sobre as opções de carregamento em massa, consulte [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
#### <a name="performance-improvements"></a>Melhorias de desempenho  
 Para melhorar o desempenho de uma inserção de massa e o acesso aos dados de tabela durante a operação de inserção em massa, você deve alterar as opções padrão conforme o seguinte:  
  
-   Não verificar restrições na tabela de destino ou exibir durante a operação de importação em massa.  
  
-   Não executar disparadores de inserção definidos na tabela de destino durante a operação de carregamento em massa.  
  
-   Não aplicar um bloqueio à tabela. Desse modo, a tabela permanece disponível para outros usuários e aplicativos durante a operação de inserção em massa.  
  
## <a name="configuration-of-the-sql-server-destination"></a>Configuração do destino do SQL Server  
 É possível configurar o destino do SQL Server das seguintes maneiras:  
  
-   Especificar a tabela ou exibir em qual carregar os dados em massa.  
  
-   Personalizar a operação de carregamento em massa especificando opções como verificar restrições ou não.  
  
-   Especificar se todas as linhas confirmam em um lote ou definem o número de máximo de linhas para confirmar como um lote.  
  
-   Especificar um tempo-limite para a operação de carregamento em massa.  
  
 Esse destino usa um gerenciador de conexões OLE DB para conectar-se a uma fonte de dados e o gerenciador de conexões especifica o provedor OLE DB a ser usado. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] também fornece o objeto de fonte de dados do qual se pode criar um administrador de conexão OLE DB. Isto torna as fontes de dados e exibições de fontes de dados disponíveis para o destino do SQL Server.  
  
 O destino do SQL Server tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](./set-the-properties-of-a-data-flow-component.md)  
  
-   [Propriedades personalizadas do destino SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Carregar dados em massa por meio do destino do SQL Server](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Carregar dados em massa por meio do destino do SQL Server](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico, [You may get "Unable to prepare the SSIS bulk insert for data insertion" error on UAC enabled systems](https://go.microsoft.com/fwlink/?LinkId=199482), em support.microsoft.com.  
  
-   Artigo técnico, [The Data Loading Performance Guide](/previous-versions/sql/sql-server-2008/dd425070(v=sql.100)), em msdn.microsoft.com.  
  
-   Artigo técnico, [Using SQL Server Integration Services to Bulk Load Data](https://go.microsoft.com/fwlink/?LinkId=233701)(Usando o SQL Server Integration Services para carregar dados em massa), em simple-talk.com.  
  
## <a name="sql-destination-editor-connection-manager-page"></a>Editor do Destino SQL (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos SQL** para especificar informações de fonte de dados e visualizar os resultados. O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega dados em tabelas ou exibições em um banco de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões OLE DB**  
 Selecione uma conexão existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
## <a name="sql-destination-editor-mappings-page"></a>Editor de Destino SQL (página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo **Editor de Destino SQL** para mapear colunas de entrada para colunas de destino.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear colunas de entrada disponíveis na tabela para as colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis na tabela para as colunas de entrada.  
  
 **Coluna de Entrada**  
 Exibir colunas de entrada selecionadas na tabela acima. É possível alterar os mapeamentos usando a lista **Colunas de Entrada Disponíveis**.  
  
 **Coluna de Destino**  
 Exiba cada coluna de destino disponível, seja ela mapeada ou não.  
  
## <a name="sql-destination-editor-advanced-page"></a>Editor de Destino SQL (página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor de Destino SQL** para especificar opções avançadas de inserção em massa.  
  
### <a name="options"></a>Opções  
 **Manter identidade**  
 Especifique se a tarefa deve inserir valores em colunas de identidade. O valor padrão dessa propriedade é **False**.  
  
 **Manter nulos**  
 Especifique se a tarefa deve manter valores nulos. O valor padrão dessa propriedade é **False**.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela deve ser bloqueada no carregamento de dados. O valor padrão dessa propriedade é **True**.  
  
 **Verificar restrições**  
 Especifique se a tarefa deve verificar restrições. O valor padrão dessa propriedade é **True**.  
  
 **Acionadores**  
 Especifique se a inserção em massa deve ativar gatilhos em tabelas. O valor padrão dessa propriedade é **False**.  
  
 **Primeira Linha**  
 Especifique a primeira linha a inserir. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades** , no **Editor Avançado** e no modelo de objeto.  
  
 **Última Linha**  
 Especifique a última linha a inserir. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades** , no **Editor Avançado** e no modelo de objeto.  
  
 **Número máximo de erros**  
 Especifique o número máximo de erros permitido antes que a inserção em massa cesse. O valor padrão desta propriedade é **-1**, indicando que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino SQL** para indicar que não deseja atribuir um valor para esta propriedade. Use -1 na janela **Propriedades** , no **Editor Avançado** e no modelo de objeto.  
  
 **Tempo Limite**  
 Especifique o tempo limite, em segundos, a ser aguardado antes de interrupção da inserção em massa.  
  
 **Ordenar colunas**  
 Digite os nomes das colunas de classificação. Cada coluna pode ser classificada em ordem crescente ou decrescente. Ao usar várias colunas de classificação, delimite a lista com vírgulas.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
