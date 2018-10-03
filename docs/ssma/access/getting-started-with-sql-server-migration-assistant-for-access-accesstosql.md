---
title: Introdução ao Assistente de migração do SQL Server para Access | Microsoft Docs
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
ms.openlocfilehash: 1168609d35a266f2ac5fe6641aee7ca131bc9d89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668664"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Introdução ao SQL Server Migration Assistant for Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para acesso permite que você converta rapidamente os objetos de banco de dados de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de BD SQL do Azure, carregue os objetos resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL DB, e migrar dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Se necessário, você também pode vincular tabelas do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em tabelas de BD SQL do Azure para que você possa continuar a usar seus aplicativos front-end do Access existentes com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.  
  
Este tópico apresenta o processo de instalação e ajuda a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, você primeiro deve instalar o programa cliente SSMA em um computador que possa acessar os bancos de dados você deseja migrar e a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Para obter instruções de instalação, consulte [instalar o SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Para iniciar o SSMA, clique em **inicie**, aponte para **todos os programas**, aponte para **SQL Server Migration Assistant for Access**e, em seguida, selecione **migração do SQL Server Assistant for Access**.  
  
## <a name="using-ssma"></a>Usando o SSMA  
Depois de instalar o SSMA, ele ajuda a se familiarizar com a interface de usuário do SSMA antes de usar a ferramenta para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. A interface do usuário do SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros são mostrados no diagrama a seguir:  
  
![SSMA para Interface gráfica do usuário de acesso](../../ssma/access/media/ssmaforaccessgui.gif "SSMA para Interface gráfica do usuário de acesso")  
  
Para iniciar uma migração, crie um novo projeto e, em seguida, adicione bancos de dados Access para o Gerenciador de metadados de acesso. Você pode, em seguida, clique com botão direito objetos no Gerenciador de metadados de acesso para executar tarefas como:
- Exportando um inventário dos objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.
- Criando relatórios que avaliam as conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.
- Convertendo esquemas de acesso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de BD SQL do Azure.

Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Após uma conexão bem-sucedida, uma hierarquia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados aparece no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Depois de converter esquemas de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, você pode selecionar esses esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e, em seguida, carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se você tiver selecionado o BD SQL do Azure da migração para a lista suspensa na caixa de diálogo Novo projeto, você deve se conectar ao BD SQL do Azure. Após uma conexão bem-sucedida, a hierarquia de bancos de dados SQL do Azure aparece no Gerenciador de metadados de banco de dados de SQL do Azure. Depois de converter esquemas de acesso aos esquemas de BD SQL do Azure, você pode selecionar esses esquemas convertidas no Gerenciador de metadados do Azure SQL DB e, em seguida, carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Depois que você carregar esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL do Azure, você pode retornar ao Gerenciador de metadados de acesso e migrar dados de bancos de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados SQL do Azure. Se necessário, você também pode vincular tabelas do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabelas de BD SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como realizá-las, consulte os tópicos a seguir:  
  
-   [Preparar bancos de dados de acesso para a migração](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [Vincular aplicativos do Access para o SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados que você pode usar para procurar e executar ações no acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados SQL do Azure.  
  
#### <a name="access-metadata-explorer"></a>Acessar Gerenciador de metadados  
Gerenciador de metadados de acesso mostra informações sobre os bancos de dados de acesso que foram adicionados ao projeto. Quando você adiciona um banco de dados, o SSMA recupera metadados sobre o banco de dados, que é os metadados que estão disponível no Gerenciador de metadados de acesso.  
  
Você pode usar o Gerenciador de metadados de acesso para executar as seguintes tarefas:  
  
-   Procure tabelas em cada banco de dados do Access.  
  
-   Selecionar objetos para a conversão e converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe. Para obter mais informações, consulte [converter objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md).  
  
-   Selecione objetos para migração de dados e migrar os dados de um desses objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [migrando dados do Access para SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
-   Vincular e desvincular o acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server ou do Gerenciador de metadados do banco de dados SQL do Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados de banco de dados de SQL do Azure mostra informações sobre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Quando você se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure, o SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar o SQL Server ou o Gerenciador de metadados de banco de dados de SQL do Azure para selecionar objetos de banco de dados do Access convertidos e carregar (Sincronizar) esses objetos na instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.  
  
Para obter mais informações, consulte [Carregando objetos de banco de dados convertidos no SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados de acesso, quatro guias aparecem: **tabela**, **mapeamento de tipo**, **propriedades**, e **dados** . Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, três guias são exibidas: **tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados de acesso, você pode alterar os mapeamentos de tipo. Certifique-se de fazer essas alterações antes de criar relatórios ou converter esquemas.  
  
-   Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você pode alterar as propriedades de tabela e índice na **tabela** guia. Faça essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [converter objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md).  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, adicionando arquivos de banco de dados do Access e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Esses botões se parecer com os comandos na **arquivo** menu.  
  
#### <a name="the-migration-toolbar"></a>A barra de ferramentas de migração  
A barra de ferramentas de migração contém os seguintes comandos:  
  
|Botão|Função|  
|----------|------------|  
|**Converter, carregar e migrar**|Converte os bancos de dados do Access, carrega os objetos convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL DB, e migra os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure, tudo em uma única etapa.|  
|**Criar relatório**|Converte o esquema de acesso selecionado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de BD SQL do Azure e, em seguida, cria um relatório que mostra a conversão foi bem-sucedida como.<br /><br />Esse comando está disponível somente quando os objetos selecionados no Gerenciador de metadados de acesso.|  
|**Converter esquema**|Converte o esquema de acesso selecionado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de BD SQL do Azure.<br /><br />Esse comando está disponível somente quando os objetos selecionados no Gerenciador de metadados de acesso.|  
|**Migrar dados**|Migra dados do banco de dados Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Antes de executar esse comando, você deve converter os esquemas de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de BD SQL do Azure e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.<br /><br />Esse comando está disponível somente quando os objetos selecionados no Gerenciador de metadados de acesso.|  
|**Parar**|Interrompe o processo atual, como converter objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de BD SQL do Azure.|  
  
### <a name="menus"></a>Menus  
O SSMA contém os seguintes menus:  
  
|Menu|Description|  
|--------|---------------|  
|**File**|Contém comandos para o Assistente de migração, trabalhando com projetos, adicionar e remover arquivos de banco de dados do Access e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel de detalhes do SQL. Para abrir o **gerenciar indicadores** caixa de diálogo, no menu Editar, clique em Gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores atuais. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados Explorers** comando. Isso sincroniza os objetos entre o Gerenciador de metadados de acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do Azure SQL DB. Também contém comandos para exibir e ocultar os **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar com os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, exportar dados, migrar dados e objetos, vincular tabelas e fornece acesso a globais e configurações de projeto de caixas de diálogo.|  
|**Ajuda**|Fornece acesso para ajudar a SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra o erro, aviso e mensagens informativas em uma lista que você pode classificar.  
  
## <a name="see-also"></a>Confira também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
