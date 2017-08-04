---
title: "Editor de destino do OLE DB (página Gerenciador de Conexão) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
caps.latest.revision: 81
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c6561914b8d059fc6ceed51a6ed82661620efca5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="ole-db-destination-editor-connection-manager-page"></a>Editor de Destino OLE DB (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de OLE DB** para selecionar a conexão OLE DB para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** do destino OLE DB não está disponível no **Editor de Destino OLE DB**, mas pode ser definida usando o **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Destino OLE DB em [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
 Para obter mais informações sobre o destino OLE DB, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Modo de acesso aos dados**  
 Especifique o método de carregamento de dados no destino. O carregamento de conjunto de caracteres de bytes duplos (DBCS) requer o uso de uma das opções de carregamento rápido. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
|Opção|Description|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma tabela ou exibição no destino OLE DB.|  
|Tabela ou exibição - carregamento rápido|Carregue dados em uma tabela ou exibição no destino OLE DB e use a opção de carregamento rápido. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Nome da tabela ou variável do nome de exibição|Especifique a tabela ou nome de exibição em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Variável do nome da tabela ou do nome de exibição - carregamento rápido|Especifique o nome da tabela ou exibição em uma variável e use a opção de carregamento rápido para carregar dados. Para obter mais informações sobre os modos de acesso aos dados de carregamento rápido que são otimizados para inserções em massa, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
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
>  Ao clicar em **Novo**, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
### <a name="data-access-mode--table-or-view--fast-load"></a>Modo de acesso aos dados = Tabela ou exibição – carregamento rápido  
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
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da tabela ou da exibição.  
  
### <a name="data-access-mode--table-name-or-view-name-variable--fast-load"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição – carregamento rápido  
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
  
### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
> [!NOTE]  
>  O destino OLE DB não aceita parâmetros. Se você precisar executar uma instrução parametrizada INSERT, considere a transformação Comando OLE DB. Para obter mais informações, consulte [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 **Build query**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino do OLE DB &#40; Página mapeamentos &#41;](../../integration-services/data-flow/ole-db-destination-editor-mappings-page.md)   
 [Editor de destino do OLE DB &#40; Página de saída de erro &#41;](../../integration-services/data-flow/ole-db-destination-editor-error-output-page.md)   
 [Carregar dados usando o destino OLE DB](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  
