---
title: Guia de Introdução com o SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11e0869f3e15c01337f2e86cb3294cbf9c94eb5b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Guia de Introdução com o SSMA para DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Assistente de migração (SSMA) para DB2 permite que você rapidamente converter esquemas de banco de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, carregue os esquemas resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migrar dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalando o SSMA  
Para usar o SSMA, primeiro instale o programa de cliente do SSMA em um computador que pode acessar o banco de dados de origem DB2 e a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Provedores OLE DB do DB2 no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses componentes oferecem suporte a migração de dados e a emulação de funções de sistema do DB2. Para obter instruções de instalação, consulte [instalando SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md).  
  
Para iniciar o SSMA, clique em **iniciar**, aponte para **todos os programas**, aponte para  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para DB2**e, em seguida, clique em  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para DB2**.  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA para Interface de usuário do DB2  
Depois que o SSMA é instalado, você pode usar o SSMA para migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de iniciar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![Interface de usuário do SSMA](../../ssma/db2/media/ssma_db2_ui.png "Interface de usuário do SSMA")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conectar a um banco de dados do DB2. Após uma conexão bem-sucedida, os esquemas de DB2 serão exibido no Gerenciador de metadados do DB2. Você pode então objetos com o botão direito no Gerenciador de metadados do DB2 para executar tarefas como criam relatórios que avaliam conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Após uma conexão bem-sucedida, uma hierarquia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados serão exibidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados. Depois de converter esquemas DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, selecione os esquemas convertidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados e, em seguida, sincronizar os esquemas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Depois de sincronizar convertidas esquemas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode retornar ao Gerenciador de metadados do DB2 e migrar dados de esquemas do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados.  
  
Para obter mais informações sobre essas tarefas e como executá-los, consulte [migração de bancos de dados DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
As seções a seguir descrevem os recursos da interface de usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações no DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados.  
  
#### <a name="db2-metadata-explorer"></a>DB2 Gerenciador de metadados  
Gerenciador de metadados de DB2 mostra informações sobre esquemas de DB2. Usando o Gerenciador de metadados do DB2, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe. Para obter mais informações, consulte [convertendo esquemas de DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
-   Selecionar tabelas para migração de dados e, em seguida, migrar os dados dessas tabelas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [migração de bancos de dados DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Gerenciador de metadados do SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados mostra informações sobre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Quando você se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados para selecionar objetos de banco de dados DB2 convertidos e, em seguida, sincronizar os objetos com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do DB2, seis guias aparecerá: **tabela**, **SQL**, **mapeamento de tipo, o relatório**, **propriedades**, e **dados**. O **relatório** guia contém informações somente depois de criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, as três guias serão exibidas: **tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do DB2, você pode alterar os procedimentos e mapeamentos de tipo. Para converter os procedimentos alterados e mapeamentos de tipo, faça alterações antes de converter esquemas.  
  
-   Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, você pode alterar o [!INCLUDE[tsql](../../includes/tsql_md.md)] para procedimentos armazenados. Para ver as alterações em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], fazer essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, conectando-se ao DB2 e para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses botões lembram os comandos no **arquivo** menu.  
  
#### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra a migração comandos da barra de ferramentas:  
  
|Botão|Função|  
|------|--------|  
|**Criar relatório**|Converte os objetos selecionados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe e, em seguida, cria um relatório que mostra a conversão foi como bem-sucedida.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do DB2.|  
|**Converter esquema**|Converte os objetos selecionados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do DB2.|  
|**Migrar dados**|Migra os dados do banco de dados DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Antes de executar esse comando, você deve converter os esquemas do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do DB2.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|Menu|Description|  
|----|-----------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectando-se ao DB2 e para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] do painel de detalhes do SQL. Também contém o **gerenciar indicadores** opção, onde você poderá ver uma lista de indicadores. Você pode usar os botões à direita da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados de pesquisadores** comando. Que sincroniza os objetos entre o Gerenciador de metadados do DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados. Também contém comandos para mostrar e ocultar o **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios e migrar objetos e dados. Também fornece acesso a **configurações globais** e **configurações de projeto** caixas de diálogo.|  
|**Ajuda**|Fornece acesso para ajudar o SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra erro, aviso e mensagens informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte também  
[Migrando dados do DB2 no SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[Referência da Interface de usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
