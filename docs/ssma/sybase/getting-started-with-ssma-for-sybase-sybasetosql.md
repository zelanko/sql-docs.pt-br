---
title: "Introdução ao SSMA for Sybase (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6a25db175cd6d67b71a0fc72bde969898e4bdadd
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-sybase-sybasetosql"></a>Introdução ao SSMA for Sybase (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Assistente de migração (SSMA) para Sybase permite a rápida converter esquemas de banco de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas do SQL Azure, carregue os esquemas resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, e migrar dados do Sybase ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-and-licensing-ssma"></a>Instalação e licenciamento do SSMA  
Para usar o SSMA, primeiro instale o programa de cliente do SSMA em um computador que possa acessar a instância de origem do Sybase ASE tanto a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Para usar a migração de dados do lado de servidor, você deve instalar o pacote de extensão e pelo menos um dos provedores Sybase (OLE DB ou ADO.NET) no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses componentes oferecem suporte a migração de dados e a emulação Sybase ASE de funções do sistema. Para obter instruções de instalação, consulte [instalando SSMA para Sybase &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Para iniciar o SSMA, clique em **iniciar**, aponte para **todos os programas**, aponte para  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para Sybase**e, em seguida, selecione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para Sybase**. Na primeira vez que você iniciar o SSMA, será exibida uma caixa de diálogo licenciamento. Você deve licenciar SSMA usando um Windows Live ID, antes de usar o SSMA. Instruções de licenciamento são incluídas com as instruções de instalação a [instalando SSMA para Sybase cliente &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) tópico.  
  
## <a name="ssma-for-sybase-user-interface"></a>SSMA para Interface do Usuário Sybase  
Depois que o SSMA é instalado e licenciado, você pode usar o SSMA para migrar bancos de dados Sybase ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de iniciar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![SSMA para Interface do usuário Sybase](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA para Interface do usuário Sybase")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conectar para Sybase ASE. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados Sybase ASE aparecerá no Gerenciador de metadados do Sybase. Você pode então objetos com o botão direito no Gerenciador de metadados do Sybase para realizar tarefas como criam relatórios que avaliam conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você também pode fazer essas tarefas por meio de menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Após uma conexão bem-sucedida, uma hierarquia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do SQL Azure aparecerá em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure. Depois de converter esquemas Sybase ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas do SQL Azure, selecione os esquemas convertidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure e, em seguida, carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
Depois de carregar esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você pode retornar ao Gerenciador de metadados do Sybase e migrar dados de bancos de dados Sybase ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do SQL Azure.  
  
Para obter mais informações sobre essas tarefas e como executá-los, consulte [migrando Sybase ASE bancos de dados para o SQL Server - banco de dados de SQL do Azure &#40; SybaseToSQL &#41; ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
As seções a seguir descrevem os recursos da interface de usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em Sybase ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do SQL Azure.  
  
#### <a name="sybase-metadata-explorer"></a>Gerenciador de metadados do Sybase  
Gerenciador de metadados do Sybase mostra informações sobre bancos de dados na instância de origem do Sybase ASE.  
  
Usando o Gerenciador de metadados do Sybase, você pode executar as seguintes tarefas:  
  
-   Procure tabelas em cada banco de dados.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Selecionar objetos para a migração de dados e, em seguida, migrar os dados desses objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Para obter mais informações, consulte [migrando dados do Sybase ASE para o SQL Server - banco de dados de SQL do Azure &#40; SybaseToSQL &#41; ](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server ou SQL Azure metadados Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ou o Gerenciador de metadados do SQL Azure mostra informações sobre uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Quando você se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, o SSMA recupera metadados sobre essa instância e as armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure para selecionar objetos de banco de dados Sybase ASE convertidos e, em seguida, carregar (synchronize) os objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
Para obter mais informações, consulte [carregar objetos de banco de dados convertidos no SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do Sybase, seis guias aparecerá: **tabela**, **SQL**, **mapeamento de tipo**, **dados, propriedades** e **relatório**. O **relatório** guia contém informações somente depois que você criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure, as três guias serão exibidas: **tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do Sybase, você pode alterar os procedimentos e mapeamentos de tipo. Você deve fazer essas alterações antes de converter esquemas.  
  
-   Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure, você pode alterar o [!INCLUDE[tsql](../../includes/tsql_md.md)] para procedimentos armazenados. Você deve fazer essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, conectando-se para Sybase ASE e para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Esses botões lembram os comandos no **arquivo** menu.  
  
#### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A barra de ferramentas de migração contém os seguintes comandos:  
  
|Botão|Função|  
|----------|------------|  
|**Criar relatório**|Converte os objetos selecionados Sybase ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe e, em seguida, cria um relatório que mostra a conversão foi como bem-sucedida.<br /><br />Este comando está disponível somente quando os objetos selecionados no Gerenciador de metadados do Sybase.|  
|**Converter esquema**|Converte os objetos selecionados do Sybase ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure.<br /><br />Este comando está disponível somente quando os objetos selecionados no Gerenciador de metadados do Sybase.|  
|**Migrar dados**|Migra os dados do banco de dados Sybase ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Antes de executar esse comando, você deve converter os esquemas do Sybase para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas do SQL Azure e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.<br /><br />Este comando está disponível somente quando os objetos selecionados no Gerenciador de metadados do Sybase.|  
|**Parar**|Interrompe o processo atual, como a conversão de objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure.|  
  
### <a name="menus"></a>Menus  
O SSMA contém os seguintes menus.  
  
|Menu|Description|  
|--------|---------------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectando-se para Sybase ASE e para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] do painel de detalhes do SQL. Também contém o **gerenciar indicadores** opção, onde você poderá ver uma lista de indicadores. Você pode usar os botões à direita da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados de pesquisadores** comando. Isso sincroniza os objetos entre o Gerenciador de metadados do Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure. Também contém comandos para exibir e ocultar o **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, exportar dados e migrar objetos e dados. Também fornece acesso a **configurações globais** e **configurações de projeto** caixas de diálogo.|  
|**Testador**|Contém comandos para criar casos de teste, exibir os resultados de teste e comandos para gerenciamento de backup do banco de dados.|  
|**Ajuda**|Fornece acesso para ajudar o SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra erro, aviso e mensagens informativas em uma lista que você pode classificar.  
  
## <a name="see-also"></a>Consulte também  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Referência de Interface do usuário &#40; SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  

