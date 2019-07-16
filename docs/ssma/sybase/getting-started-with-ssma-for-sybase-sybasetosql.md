---
title: Introdução ao SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f07f230f52fee5707084c01060e92220b35cb75c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029117"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>Introdução ao SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA (Migration Assistant) para o SAP ASE permite que você rapidamente esquemas de banco de dados do SAP Adaptive Server Enterprise (ASE) para converter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de banco de dados SQL, carregar os esquemas resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL Azure, e migrar os dados SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL do Azure.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-and-licensing-ssma"></a>Instalação e licenciamento do SSMA  
Para usar o SSMA, você primeiro deve instalar o programa cliente SSMA em um computador que possa acessar a instância de origem do SAP ASE tanto a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Para usar a migração de dados do lado do servidor, você deve instalar o pacote de extensão e pelo menos um dos provedores do SAP ASE (OLE DB ou ADO.NET) no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes oferecem suporte a migração de dados e a emulação de funções de sistema do SAP ASE. Para obter instruções de instalação, consulte [instalar o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Para iniciar o SSMA, clique em **inicie**, aponte para **todos os programas**, aponte para  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase**e, em seguida, selecione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para o Sybase**. Na primeira vez que você inicie o SSMA, será exibida uma caixa de diálogo de licenciamento. Você deve licenciar SSMA usando um Windows Live ID antes de usar o SSMA. Instruções de licenciamento estão incluídas com as instruções de instalação nos [instalar o SSMA para Sybase cliente &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) tópico.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA para interface de usuário do SAP ASE  
Depois que o SSMA é instalado e licenciado, você pode usar o SSMA para migrar bancos de dados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![O SSMA para Interface do usuário do ASE SAP](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA para Interface do usuário do ASE SAP")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conectar ao SAP ASE. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do SAP ASE será exibido no Gerenciador de metadados do Sybase. Você pode então objetos do botão direito do mouse no Gerenciador de metadados do Sybase para realizar tarefas como criar relatórios que avaliam as conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Você também pode realizar essas tarefas por meio de menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Após uma conexão bem-sucedida, uma hierarquia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados SQL do Azure aparecerá no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure. Depois de converter esquemas do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de banco de dados SQL, selecione as esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure e, em seguida, carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL.  
  
Depois que você carregar esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL Azure, você pode retornar ao Gerenciador de metadados do Sybase e migrar dados de bancos de dados do SAP ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como realizá-las, consulte [migrando SAP ASE bancos de dados para o SQL Server - banco de dados SQL &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em SAP ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados SQL do Azure.  
  
#### <a name="sybase-metadata-explorer"></a>Gerenciador de metadados do Sybase  
Gerenciador de metadados do Sybase mostra informações sobre bancos de dados na instância de origem do SAP ASE.  
  
Usando o Gerenciador de metadados do Sybase, você pode executar as seguintes tarefas:  
  
-   Procure tabelas em cada banco de dados.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de banco de dados SQL. Para obter mais informações, consulte [converter objetos de banco de dados do SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Selecione objetos para migração de dados e, em seguida, migrar os dados desses objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Para obter mais informações, consulte [migrando dados do SAP ASE no SQL Server - banco de dados SQL &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server ou do Gerenciador de metadados do SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure mostra informações sobre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Quando você se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL, o SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure para selecionar objetos de banco de dados do SAP ASE convertidos e, em seguida, carregar (Sincronizar) esses objetos na instância da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL.  
  
Para obter mais informações, consulte [Carregando objetos de banco de dados convertidos no SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do Sybase, seis guias aparecem: **Tabela**, **SQL**, **mapeamento de tipo**, **dados**, **propriedades**, e **relatório**. O **relatório** guia contém informações somente depois de criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure, três guias são exibidas: **Tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do Sybase, você pode alterar procedimentos e mapeamentos de tipo. Faça essas alterações antes de converter esquemas.  
  
-   Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Gerenciador de metadados do SQL Azure, você pode alterar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para procedimentos armazenados. Faça essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, conectar-se ao SAP ASE e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Esses botões se parecer com os comandos na **arquivo** menu.  
  
#### <a name="the-migration-toolbar"></a>A barra de ferramentas de migração  
A barra de ferramentas de migração contém os seguintes comandos:  
  
|Botão|Função|  
|----------|------------|  
|**Criar relatório**|Converte os objetos selecionados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, cria um relatório que mostra a conversão foi bem-sucedida como.<br /><br />Esse comando está disponível somente quando os objetos selecionados no Gerenciador de metadados do Sybase.|  
|**Converter esquema**|Converte os objetos selecionados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados SQL.<br /><br />Esse comando está disponível somente quando os objetos selecionados no Gerenciador de metadados do Sybase.|  
|**Migrar dados**|Migra dados do banco de dados SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Antes de executar esse comando, você deve converter os esquemas do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas de banco de dados SQL e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL.<br /><br />Esse comando está disponível somente quando os objetos selecionados no Gerenciador de metadados do Sybase.|  
|**Parar**|Interrompe o processo atual, como converter objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de banco de dados SQL.|  
  
### <a name="menus"></a>Menus  
O SSMA contém os seguintes menus:  
  
|Menu|Descrição|  
|--------|---------------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectar-se ao SAP ASE e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel de detalhes do SQL. Também contém o **gerenciar indicadores** opção, onde você pode ver uma lista de indicadores atuais. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados Explorers** comando. Isso sincroniza os objetos entre o Gerenciador de metadados do Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure. Também contém comandos para exibir e ocultar os **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, exportar dados e migrar objetos e dados. Também fornece acesso para o **configurações globais** e **configurações do projeto** caixas de diálogo.|  
|**Testador**|Contém comandos para criar casos de teste, exibir resultados de teste e comandos para gerenciamento de backup do banco de dados.|  
|**Ajuda**|Fornece acesso para ajudar a SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra o erro, aviso e mensagens informativas em uma lista que você pode classificar.  
  
## <a name="see-also"></a>Confira também  
[Migrando SAP ASE bancos de dados SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Referência da Interface do usuário &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
