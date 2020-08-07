---
title: Introdução com o SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
description: Saiba mais sobre o processo de instalação do SSMA (Assistente de Migração do SQL Server) para SAP ASE e familiarize-se com a interface do usuário do SSMA.
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cd6e32470673a87a410530298972b251d2807e4b
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931806"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>Introdução com o SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Assistente de Migração (SSMA) para SAP ASE permite que você converta rapidamente esquemas de banco de dados do SAP Adaptive Server Enterprise (ASE) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas de banco de dados SQL do Azure, carregue os esquemas resultantes no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL do Azure, e migre-os do SAP ase para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface do usuário do SSMA.  
  
## <a name="installing-and-licensing-ssma"></a>Instalando e licenciando o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa cliente do SSMA em um computador que possa acessar a instância de origem do SAP ASE e a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do banco de dados SQL do Azure. Para usar a migração de dados do lado do servidor, você deve instalar o pacote de extensão e pelo menos um dos provedores do SAP ASE (OLE DB ou ADO.NET) no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses componentes dão suporte à migração de dados e à emulação de funções do sistema SAP ASE. Para obter instruções de instalação, consulte [instalando o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Para iniciar o SSMA, clique em **Iniciar**, aponte para **todos os programas**, aponte para ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para Sybase**e, em seguida, selecione ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para Sybase**. Na primeira vez que você iniciar o SSMA, uma caixa de diálogo licenciamento será exibida. Você deve licenciar o SSMA usando um Windows Live ID antes de poder usar o SSMA. As instruções de licenciamento estão incluídas nas instruções de instalação no tópico [Installing SSMA for Sybase Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) .  
  
## <a name="ssma-for-sap-ase-user-interface"></a>Interface do usuário do SSMA para SAP ASE  
Depois que o SSMA for instalado e licenciado, você poderá usar o SSMA para migrar bancos de dados do SAP ASE para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL do Azure. Ele ajuda a se familiarizar com a interface do usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![Interface do usuário do SSMA para SAP ASE](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "Interface do usuário do SSMA para SAP ASE")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conecta ao SAP ASE. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do SAP ASE será exibida no Gerenciador de metadados do Sybase. Em seguida, você pode clicar com o botão direito do mouse em objetos no Gerenciador de metadados do Sybase para executar tarefas como criar relatórios que avaliam conversões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no banco de dados SQL do Azure. Você também pode fazer essas tarefas por meio das barras de ferramentas e menus.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL do Azure. Após uma conexão bem-sucedida, uma hierarquia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou bancos de dados SQL do Azure aparecerão no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure o Gerenciador de metadados. Depois de converter esquemas do SAP ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas do ou do banco de dados SQL do Azure, selecione os esquemas convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure Gerenciador de metadados e, em seguida, carregue os esquemas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados SQL do Azure ou.  
  
Depois de carregar os esquemas convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no banco de dados SQL do Azure, você pode retornar ao Gerenciador de metadados do Sybase e migrar dados de bancos de dados do SAP ase para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para bancos de dado SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e sobre como executá-las, consulte [migrando bancos de dados do SAP ase para SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em bancos de dados do SAP ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Azure SQL.  
  
#### <a name="sybase-metadata-explorer"></a>Gerenciador de metadados Sybase  
O Gerenciador de metadados do Sybase mostra informações sobre bancos de dados na instância de origem do SAP ASE.  
  
Usando o Gerenciador de metadados do Sybase, você pode executar as seguintes tarefas:  
  
-   Procure as tabelas em cada banco de dados.  
  
-   Selecione objetos para conversão e converta os objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a sintaxe do banco de dados SQL do Azure. Para obter mais informações, consulte [convertendo objetos de banco de dados SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Selecione objetos para migração de dados e, em seguida, migre os dados desses objetos para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database. Para obter mais informações, consulte [migrando dados do SAP ase para o SQL Server-banco de SYBASETOSQL SQL do Azure &#40;o&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server ou SQL Azure o Gerenciador de metadados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou SQL Azure Gerenciador de metadados mostra informações sobre uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL do Azure. Quando você se conecta a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL do Azure, o SSMA recupera metadados sobre essa instância e as armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure o Gerenciador de metadados para selecionar objetos de banco de dados SAP ase convertidos e, em seguida, carregar (sincronizar) esses objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no banco de dados SQL do Azure.  
  
Para obter mais informações, consulte [carregando objetos de banco de dados convertidos em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados estão as guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do Sybase, seis guias serão exibidas: **tabela**, **SQL**, **mapeamento de tipo**, **dados**, **Propriedades**e **relatório**. A guia **relatório** contém informações somente depois que você cria um relatório que contém o objeto selecionado. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure o Gerenciador de metadados, serão exibidas três guias: **tabela**, **SQL**e **dados**.  
  
A maioria das configurações de metadados é somente leitura. No entanto, você pode alterar os seguintes metadados:  
  
-   No Gerenciador de metadados do Sybase, você pode alterar os procedimentos e os mapeamentos de tipo. Faça essas alterações antes de converter os esquemas.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure Gerenciador de metadados, você pode alterar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para procedimentos armazenados. Faça essas alterações antes de carregar os esquemas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas de projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, conectar-se ao SAP ASE e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao banco de dados SQL do Azure. Esses botões se assemelham aos comandos no menu **arquivo** .  
  
#### <a name="the-migration-toolbar"></a>A barra de ferramentas de migração  
A barra de ferramentas de migração contém os seguintes comandos:  
  
|Botão|Função|  
|----------|------------|  
|**Criar Relatório**|Converte os objetos selecionados do SAP ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, cria um relatório que mostra a êxito da conversão.<br /><br />Esse comando está disponível somente quando objetos são selecionados no Gerenciador de metadados do Sybase.|  
|**Converter esquema**|Converte os objetos do SAP ASE selecionados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do banco de dados SQL do Azure.<br /><br />Esse comando está disponível somente quando objetos são selecionados no Gerenciador de metadados do Sybase.|  
|**Migrar dados**|Migra dados do banco de dados do SAP ASE para o ou do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL do Azure. Antes de executar esse comando, você deve converter os esquemas do SAP ASE no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas do banco de dados SQL do Azure e, em seguida, carregar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no banco de dados SQL do Azure.<br /><br />Esse comando está disponível somente quando objetos são selecionados no Gerenciador de metadados do Sybase.|  
|**Parar**|Interrompe o processo atual, como conversão de objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe do banco de dados SQL do Azure.|  
  
### <a name="menus"></a>Menus  
O SSMA contém os seguintes menus:  
  
|Menu|Descrição|  
|--------|---------------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectar-se ao SAP ASE e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou ao banco de dados SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel detalhes do SQL. Também contém a opção **gerenciar indicadores** , em que você pode ver uma lista de indicadores existentes. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o comando **sincronizar gerenciadores de metadados** . Isso sincroniza os objetos entre o Gerenciador de metadados Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure o Gerenciador de metadados. Também contém comandos para exibir e ocultar os painéis de **saída** e de **lista de erros** e um **layout** de opção para gerenciar os layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, exportar dados e migrar objetos e dados. Também fornece acesso às caixas de diálogo **configurações globais** e **configurações do projeto** .|  
|**Testador**|Contém comandos para criar casos de teste, exibir resultados de teste e comandos para o gerenciamento de backup de banco de dados.|  
|**Ajuda**|Fornece acesso à ajuda do SSMA e à caixa de diálogo **sobre** .|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e painel de Lista de Erros  
O menu **Exibir** fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel saída mostra mensagens de status do SSMA durante a conversão de objetos, a sincronização de objetos e a migração de dados.  
  
-   O painel de Lista de Erros mostra mensagens de erro, aviso e informativas em uma lista que você pode classificar.  
  
## <a name="see-also"></a>Consulte também  
[Migrar bancos de dados do SAP ASE para o SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Referência da interface do usuário &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
