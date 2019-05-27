---
title: Editor de destino do OLE DB (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 436b758abdde0c05539bc17aabd2c11b240642df
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057143"
---
# <a name="ole-db-destination-editor-connection-manager-page"></a>Editor de Destino OLE DB (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de OLE DB** para selecionar a conexão OLE DB para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
> [!NOTE]  
>  O `CommandTimeout` propriedade do destino OLE DB não está disponível na **Editor de destino do OLE DB**, mas pode ser definida usando a **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Destino OLE DB em [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md).  
  
 Para obter mais informações sobre o destino OLE DB, consulte [OLE DB Destination](data-flow/ole-db-destination.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Modo de acesso aos dados**  
 Especifique o método de carregamento de dados no destino. O carregamento de conjunto de caracteres de bytes duplos (DBCS) requer o uso de uma das opções de carregamento rápido. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](data-flow/ole-db-destination.md).  
  
|Opção|Descrição|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma tabela ou exibição no destino OLE DB.|  
|Tabela ou exibição - carregamento rápido|Carregue dados em uma tabela ou exibição no destino OLE DB e use a opção de carregamento rápido. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](data-flow/ole-db-destination.md).|  
|Nome da tabela ou variável do nome de exibição|Especifique a tabela ou nome de exibição em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)|  
|Variável do nome da tabela ou do nome de exibição - carregamento rápido|Especifique o nome da tabela ou exibição em uma variável e use a opção de carregamento rápido para carregar dados. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](data-flow/ole-db-destination.md).|  
|Comando SQL|Carregue dados no destino OLE DB usando uma consulta SQL.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
## <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
 Cada uma das configurações do **Modo de acesso aos dados** exibe um conjunto de opções dinâmicas específico àquela configuração. As seções a seguir descrevem todas as opções dinâmicas disponíveis de cada configuração de **Modo de acesso aos dados** .  
  
### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da tabela ou da exibição**  
 Selecione o nome da tabela ou da exibição na lista de tabelas ou exibições disponíveis na fonte de dados.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
### <a name="data-access-mode--table-or-view---fast-load"></a>Modo de acesso a dados = tabela ou exibição – carregamento rápido  
 **Nome da tabela ou exibição**  
 Selecione uma tabela ou exibição do banco de dados nessa lista ou crie uma nova tabela clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Manter identidade**  
 Especifique se os valores de identidade serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é `false`.  
  
 **Manter nulos**  
 Especifique se os valores nulos serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é `false`.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela será bloqueada durante o carregamento. O valor padrão dessa propriedade é `true`.  
  
 **Verificar restrições**  
 Especifique se o destino verificará as restrições quando os dados forem carregados. O valor padrão dessa propriedade é `true`.  
  
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
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>Modo de acesso a dados = Variável do nome da tabela ou do nome de exibição – carregamento rápido)  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
 **Nova**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Manter identidade**  
 Especifique se os valores de identidade serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é `false`.  
  
 **Manter nulos**  
 Especifique se os valores nulos serão copiados quando os dados forem carregados. Essa propriedade só estará disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é `false`.  
  
 **Bloqueio de tabela**  
 Especifique se a tabela será bloqueada durante o carregamento. O valor padrão dessa propriedade é `false`.  
  
 **Verificar restrições**  
 Especifique se a tarefa verificará as restrições. O valor padrão dessa propriedade é `false`.  
  
 **Linhas por lote**  
 Especifique o número de linhas em um lote. O valor padrão dessa propriedade é **-1**, que indica que nenhum valor foi atribuído.  
  
> [!NOTE]  
>  Limpe a caixa de texto no **Editor de Destino de OLE DB** para indicar que você não deseja atribuir um valor personalizado para essa propriedade.  
  
 **Tamanho máximo de confirmação de inserção**  
 Especifique o tamanho do lote que o destino OLE DB tenta confirmar durante as operações de carregamento rápido. O valor padrão **2147483647** indica que todos os dados serão confirmados em um único lote depois que todas as linhas forem processadas.  
  
> [!NOTE]  
>  O valor **0** pode fazer com que o pacote em execução deixe de responder se o destino OLE DB e outro componente de fluxo de dados estiverem atualizando a mesma tabela de origem. Para impedir que o pacote pare, defina a opção **Tamanho máximo de confirmação de inserção** como **2147483647**.  
  
### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
> [!NOTE]  
>  O destino OLE DB não aceita parâmetros. Se você precisar executar uma instrução parametrizada INSERT, considere a transformação Comando OLE DB. Para obter mais informações, consulte [OLE DB Command Transformation](data-flow/transformations/ole-db-command-transformation.md).  
  
 **Construir consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destino de OLE DB &#40;Página Mapeamentos&#41;](../../2014/integration-services/ole-db-destination-editor-mappings-page.md)   
 [Editor de Destino OLE DB &#40;Página Saída de Erro&#41;](../../2014/integration-services/ole-db-destination-editor-error-output-page.md)   
 [Carregar dados por meio do destino OLE DB](data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  
