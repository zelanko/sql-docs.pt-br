---
title: Introdução com o SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0eab4f23e342c95d83baa70dd03aba2f5d4bc8d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989642"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Introdução com o SSMA para DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para DB2 permite converter rapidamente esquemas de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 em esquemas, carregar os esquemas resultantes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em e migrar dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 para o.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface do usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa cliente do SSMA em um computador que possa acessar o banco de dados DB2 de origem e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a instância de destino do. Provedores OLEDB do DB2 no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o. Esses componentes dão suporte à migração de dados e à emulação de funções do sistema DB2. Para obter instruções de instalação, consulte [instalando o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md).  
  
Para iniciar o SSMA, clique em **Iniciar**, aponte para **todos os programas**, aponte para ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assistente de migração para DB2**e clique em ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assistente de migração para DB2**.  
  
## <a name="ssma-for-db2-user-interface"></a>Interface do usuário do SSMA para DB2  
Após a instalação do SSMA, você pode usar o SSMA para migrar bancos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dados DB2 para o. Ele ajuda a se familiarizar com a interface do usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![Interface de usuário do SSMA](../../ssma/db2/media/ssma_db2_ui.png "Interface de usuário do SSMA")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conecta a um banco de dados DB2. Após uma conexão bem-sucedida, os esquemas do DB2 aparecerão no Gerenciador de metadados do DB2. Você pode clicar com o botão direito do mouse em objetos no Gerenciador de metadados do DB2 para executar tarefas como criar relatórios que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]avaliam conversões no. Você também pode executar essas tarefas usando as barras de ferramentas e menus.  
  
Você também deve se conectar a uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Após uma conexão bem-sucedida, uma hierarquia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados será exibida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Depois de converter os esquemas do DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em esquemas, selecione os esquemas convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e sincronize os esquemas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Depois de sincronizar os esquemas convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com o, você pode retornar ao Gerenciador de metadados do DB2 e migrar os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados dos esquemas do DB2 para os bancos de dado.  
  
Para obter mais informações sobre essas tarefas e como executá-las, consulte [migrando bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 e bancos de dados.  
  
#### <a name="db2-metadata-explorer"></a>Gerenciador de metadados do DB2  
O Gerenciador de metadados do DB2 mostra informações sobre os esquemas do DB2. Usando o Gerenciador de metadados do DB2, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecione objetos para conversão e converta os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe. Para obter mais informações, consulte [convertendo esquemas do DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
-   Selecione tabelas para migração de dados e migre os dados dessas tabelas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o. Para obter mais informações, consulte [migrando bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server Gerenciador de metadados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Gerenciador de metadados mostra informações sobre uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instância do. Quando você se conecta a uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do, o SSMA recupera metadados sobre essa instância e as armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Gerenciador de metadados para selecionar objetos de banco de dados DB2 convertidos e, em seguida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sincronizar esses objetos com a instância do.  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados estão as guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do DB2, seis guias serão exibidas: **tabela**, **SQL**, **mapeamento de tipo, relatório**, **Propriedades**e **dados**. A guia **relatório** contém informações somente depois que você cria um relatório que contém o objeto selecionado. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, três guias serão exibidas: **tabela**, **SQL**e **dados**.  
  
A maioria das configurações de metadados é somente leitura. No entanto, você pode alterar os seguintes metadados:  
  
-   No Gerenciador de metadados do DB2, você pode alterar os procedimentos e os mapeamentos de tipo. Para converter os procedimentos alterados e os mapeamentos de tipo, faça alterações antes de converter os esquemas.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você pode alterar [!INCLUDE[tsql](../../includes/tsql-md.md)] o para procedimentos armazenados. Para ver essas alterações no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], faça essas alterações antes de carregar os esquemas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas de projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 e conectar-se ao. Esses botões se assemelham aos comandos no menu **arquivo** .  
  
#### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra os comandos da barra de ferramentas de migração:  
  
|Botão|Função|  
|------|--------|  
|**Criar Relatório**|Converte os objetos do DB2 selecionados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sintaxe e cria um relatório que mostra a êxito da conversão.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados do DB2.|  
|**Converter esquema**|Converte os objetos do DB2 selecionados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em objetos.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados do DB2.|  
|**Migrar dados**|Migra dados do banco de dados DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o. Antes de executar esse comando, você deve converter os esquemas do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas e, em seguida, carregar os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados do DB2.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|Menu|DESCRIÇÃO|  
|----|-----------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectar-se ao DB2 e conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-se ao.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel detalhes do SQL. Também contém a opção **gerenciar indicadores** , em que você poderá ver uma lista de indicadores existentes. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o comando **sincronizar gerenciadores de metadados** . Isso sincroniza os objetos entre o Gerenciador de metadados DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Gerenciador de metadados. Também contém comandos para mostrar e ocultar os painéis de **saída** e de **lista de erros** e um **layout** de opção para gerenciar os layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios e migrar objetos e dados. Também fornece acesso às caixas de diálogo **configurações globais** e **configurações do projeto** .|  
|**Ajuda**|Fornece acesso à ajuda do SSMA e à caixa de diálogo **sobre** .|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e painel de Lista de Erros  
O menu **Exibir** fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel saída mostra mensagens de status do SSMA durante a conversão de objetos, a sincronização de objetos e a migração de dados.  
  
-   O painel de Lista de Erros mostra mensagens de erro, aviso e informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte Também  
[Migrar dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[Referência da interface do usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
