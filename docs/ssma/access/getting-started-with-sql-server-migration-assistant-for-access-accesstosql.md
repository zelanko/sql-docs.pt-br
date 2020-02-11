---
title: Introdução ao Assistente de Migração do SQL Server para acesso | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 863e62dc9e2970f7531bba15f7242c73c5b0f9e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68259921"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Introdução ao Assistente de Migração do SQL Server para acesso (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para acesso permite que você converta rapidamente objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados do Access ou objetos de BD SQL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure, carregue os objetos resultantes no ou no banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados SQL do Azure, e migre os dados de acesso ao ou ao banco de dado SQL do Azure. Se necessário, você também pode vincular tabelas de acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ou tabelas de BD SQL do Azure para que possa continuar usando seus aplicativos de front-end de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acesso existentes com o ou o banco de BD SQL do Azure.  
  
Este tópico apresenta o processo de instalação e ajuda a familiarizar você com a interface do usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa cliente do SSMA em um computador que possa acessar ambos os bancos de dados que você deseja migrar e a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância de destino do ou do banco de dados SQL do Azure. Para obter instruções de instalação, consulte [installing assistente de migração do SQL Server for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Para iniciar o SSMA, clique em **Iniciar**, aponte para **todos os programas**, aponte para **Assistente de migração do SQL Server para acesso**e, em seguida, selecione **Assistente de migração do SQL Server para acesso**.  
  
## <a name="using-ssma"></a>Usando o SSMA  
Depois de instalar o SSMA, ele ajuda a se familiarizar com a interface do usuário do SSMA antes de usar a ferramenta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migrar bancos de dados do Access para o ou o BD SQL do Azure. A interface do usuário do SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros, é mostrada no diagrama a seguir:  
  
![SSMA para Interface Gráfica do Usuário de Acesso](../../ssma/access/media/ssmaforaccessgui.gif "SSMA para Interface Gráfica do Usuário de Acesso")  
  
Para iniciar uma migração, crie um novo projeto e, em seguida, adicione bancos de dados do Access para acessar o Gerenciador de metadados. Em seguida, você pode clicar com o botão direito do mouse em objetos no Gerenciador de metadados do Access para executar tarefas como:
- Exportar um inventário de objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados do Access para o ou o BD SQL do Azure.
- Criação de relatórios que avaliam conversões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ou no banco de BD SQL do Azure.
- Convertendo esquemas de acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ou esquemas de BD SQL do Azure.

Você também pode executar essas tarefas usando as barras de ferramentas e menus.  
  
Você também deve se conectar a uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Após uma conexão bem-sucedida, uma hierarquia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados aparece no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Depois de converter esquemas de acesso em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, você pode selecionar esses esquemas convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e, em seguida, carregar os esquemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no.  
  
Se você tiver selecionado BD SQL do Azure na caixa de diálogo migrar para o menu suspenso no novo projeto, deverá se conectar ao BD SQL do Azure. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do Azure SQL DB aparece no Gerenciador de metadados do BD SQL do Azure. Depois de converter os esquemas de acesso nos esquemas do BD SQL do Azure, você pode selecionar esses esquemas convertidos no Gerenciador de metadados do banco de BD SQL do Azure e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em seguida, carregar os esquemas no.  
  
Depois de carregar os esquemas convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ou no banco de dados SQL do Azure, você pode retornar para acessar o Gerenciador de metadados e migrar dados de bancos de dado do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou bancos de dados do Azure SQL DB. Se necessário, você também pode vincular tabelas de acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ou tabelas de banco de BD SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como executá-las, consulte os seguintes tópicos:  
  
-   [Preparar bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [Vinculando aplicativos de acesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados que você pode usar para navegar e executar ações em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados do Access e do Azure SQL DB.  
  
#### <a name="access-metadata-explorer"></a>Acessar Gerenciador de metadados  
O Gerenciador de metadados do Access mostra informações sobre os bancos de dados do Access que foram adicionados ao projeto. Quando você adiciona um banco de dados do Access, o SSMA recupera metadados sobre esse banco de dados, que são os metadados disponíveis no Gerenciador de metadados do Access.  
  
Você pode usar o Gerenciador de metadados do Access para executar as seguintes tarefas:  
  
-   Procure as tabelas em cada banco de dados do Access.  
  
-   Selecione objetos para conversão e converta os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sintaxe. Para obter mais informações, consulte [convertendo objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md).  
  
-   Selecione objetos para migração de dados e migre os dados desses objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o. Para obter mais informações, consulte [migrando dados do Access para o SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
-   Vincular e desvincular o acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as tabelas.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server ou o Gerenciador de metadados do BD SQL do Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou o Gerenciador de metadados do banco de dados SQL do Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra informações sobre uma instância do ou o banco de dados SQL do Azure. Quando você se conecta a uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do ou ao banco de BD SQL do Azure, o SSMA recupera metadados sobre essa instância e as armazena no arquivo de projeto.  
  
Você pode usar o SQL Server ou o Gerenciador de metadados do BD SQL do Azure para selecionar objetos de banco de dados de acesso convertidos e carregar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sincronizar) esses objetos na instância do ou no BD SQL do Azure.  
  
Para obter mais informações, consulte [carregando objetos de banco de dados convertidos em SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados estão as guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do Access, quatro guias serão exibidas: **tabela**, **mapeamento de tipo**, **Propriedades**e **dados**. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, três guias serão exibidas: **tabela**, **SQL**e **dados**.  
  
A maioria das configurações de metadados é somente leitura. No entanto, você pode alterar os seguintes metadados:  
  
-   No Gerenciador de metadados do Access, você pode alterar os mapeamentos de tipo. Certifique-se de fazer essas alterações antes de criar relatórios ou converter esquemas.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você pode alterar as propriedades de tabela e índice na guia **tabela** . faça essas alterações antes de carregar os esquemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no. Para obter mais informações, consulte [convertendo objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md).  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas de projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, adicionar arquivos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados do Access e conectar-se ao ou ao BD SQL do Azure. Esses botões se assemelham aos comandos no menu **arquivo** .  
  
#### <a name="the-migration-toolbar"></a>A barra de ferramentas de migração  
A barra de ferramentas de migração contém os seguintes comandos:  
  
|Botão|Função|  
|----------|------------|  
|**Converter, carregar e migrar**|Converte os bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Access, carrega os objetos convertidos no ou no BD SQL do Azure e, em uma única etapa, faz a migração.|  
|**Criar Relatório**|Converte o esquema de acesso selecionado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ou a sintaxe do banco de BD SQL do Azure e, em seguida, cria um relatório que mostra a êxito da conversão.<br /><br />Esse comando está disponível somente quando objetos são selecionados no Gerenciador de metadados do Access.|  
|**Converter esquema**|Converte o esquema de acesso selecionado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ou esquemas de BD SQL do Azure.<br /><br />Esse comando está disponível somente quando objetos são selecionados no Gerenciador de metadados do Access.|  
|**Migrar dados**|Migra dados do banco de dados do Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou o BD SQL do Azure. Antes de executar esse comando, você deve converter os esquemas de acesso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de BD SQL do Azure e, em seguida, carregar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os objetos no banco de BD SQL ou no Azure.<br /><br />Esse comando está disponível somente quando objetos são selecionados no Gerenciador de metadados do Access.|  
|**Parar**|Interrompe o processo atual, como conversão de objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe do banco de BD SQL do Azure.|  
  
### <a name="menus"></a>Menus  
O SSMA contém os seguintes menus:  
  
|Menu|DESCRIÇÃO|  
|--------|---------------|  
|**Arquivo**|Contém comandos para o assistente de migração, trabalhando com projetos, adicionando e removendo arquivos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Access e conectando-se ao ou ao BD SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel detalhes do SQL. Para abrir a caixa de diálogo **gerenciar indicadores** , no menu Editar, clique em gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores existentes. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o comando **sincronizar gerenciadores de metadados** . Isso sincroniza os objetos entre o Gerenciador de metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access e o Gerenciador de metadados do banco de BD SQL do Azure. Também contém comandos para exibir e ocultar os painéis de **saída** e de **lista de erros** e um **layout** de opção para gerenciar com os layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, exportar dados, migrar objetos e dados, vincular tabelas e fornecer acesso às caixas de diálogo de configurações globais e de projeto.|  
|**Ajuda**|Fornece acesso à ajuda do SSMA e à caixa de diálogo **sobre** .|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e painel de Lista de Erros  
O menu **Exibir** fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel saída mostra mensagens de status do SSMA durante a conversão de objetos, a sincronização de objetos e a migração de dados.  
  
-   O painel de Lista de Erros mostra mensagens de erro, aviso e informativas em uma lista que você pode classificar.  
  
## <a name="see-also"></a>Confira também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
