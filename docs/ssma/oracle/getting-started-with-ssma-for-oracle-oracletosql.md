---
title: Introdução com o SSMA para Oracle (OracleToSQL) | Microsoft Docs
description: Saiba mais sobre o processo de instalação do Assistente de Migração do SQL Server (SSMA) para Oracle e familiarize-se com a interface do usuário do SSMA.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 985d6e58d00dee705a684b7ef2f6516a5459f0df
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293863"
---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>Introdução ao SSMA para Oracle (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para Oracle permite converter rapidamente esquemas de banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, carregar os esquemas resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do Oracle para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface do usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa cliente do SSMA em um computador que possa acessar o banco de dados Oracle de origem e a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em seguida, você deve instalar um pacote de extensão e pelo menos um dos provedores Oracle (OLE DB ou [!INCLUDE[vstecado](../../includes/vstecado_md.md)] ) no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses componentes dão suporte à migração de dados e à emulação de funções do sistema Oracle. Para obter instruções de instalação, consulte [instalando o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md).  
  
Para iniciar o SSMA, clique em **Iniciar**, aponte para **todos os programas**, aponte para ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de Migração para Oracle**e clique em ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para Oracle**.  
  
## <a name="ssma-for-oracle-user-interface"></a>Interface do usuário do SSMA para Oracle  
Após a instalação do SSMA, você pode usar o SSMA para migrar bancos de dados Oracle para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ele ajuda a se familiarizar com a interface do usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![SSMA para UI Oracle](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA para UI Oracle")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conecta a um banco de dados Oracle. Após uma conexão bem-sucedida, os esquemas Oracle serão exibidos no Gerenciador de metadados Oracle. Você pode clicar com o botão direito do mouse em objetos no Gerenciador de metadados Oracle para executar tarefas como criar relatórios que avaliam conversões no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você também pode executar essas tarefas usando as barras de ferramentas e menus.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Após uma conexão bem-sucedida, uma hierarquia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados será exibida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Depois de converter os esquemas Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, selecione os esquemas convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e sincronize os esquemas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Depois de sincronizar os esquemas convertidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode retornar ao Gerenciador de metadados Oracle e migrar os dados dos esquemas Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os bancos de dado.  
  
Para obter mais informações sobre essas tarefas e como executá-las, consulte [migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados e Oracle.  
  
#### <a name="oracle-metadata-explorer"></a>Gerenciador de metadados Oracle  
O Gerenciador de metadados Oracle mostra informações sobre esquemas Oracle. Usando o Gerenciador de metadados da Oracle, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecione objetos para conversão e converta os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe. Para obter mais informações, consulte [convertendo esquemas Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
-   Selecione tabelas para migração de dados e migre os dados dessas tabelas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [migrando dados do Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server Gerenciador de metadados  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Gerenciador de metadados mostra informações sobre uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você se conecta a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o SSMA recupera metadados sobre essa instância e as armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Gerenciador de metadados para selecionar objetos de banco de dados Oracle convertidos e, em seguida, sincronizar esses objetos com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Para obter mais informações, consulte [carregando objetos de banco de dados convertidos em SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados estão as guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados Oracle, seis guias serão exibidas: **tabela**, **SQL**, **mapeamento de tipo, relatório**, **Propriedades**e **dados**. A guia **relatório** contém informações somente depois que você cria um relatório que contém o objeto selecionado. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, três guias serão exibidas: **tabela**, **SQL**e **dados**.  
  
A maioria das configurações de metadados é somente leitura. No entanto, você pode alterar os seguintes metadados:  
  
-   No Gerenciador de metadados Oracle, você pode alterar os procedimentos e os mapeamentos de tipo. Para converter os procedimentos alterados e os mapeamentos de tipo, faça alterações antes de converter os esquemas.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você pode alterar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para procedimentos armazenados. Para ver essas alterações no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , faça essas alterações antes de carregar os esquemas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas de projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, conectar-se ao Oracle e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses botões se assemelham aos comandos no menu **arquivo** .  
  
#### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra os comandos da barra de ferramentas de migração:  
  
|Botão|Função|  
|------|--------|  
|**Criar Relatório**|Converte os objetos Oracle selecionados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, cria um relatório que mostra a êxito da conversão.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados Oracle.|  
|**Converter esquema**|Converte os objetos Oracle selecionados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados Oracle.|  
|**Migrar dados**|Migra dados do Oracle Database para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Antes de executar esse comando, você deve converter os esquemas Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas e, em seguida, carregar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados Oracle.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|Menu|Descrição|  
|----|-----------|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectar-se ao Oracle e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel detalhes do SQL. Também contém a opção **gerenciar indicadores** , em que você poderá ver uma lista de indicadores existentes. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o comando **sincronizar gerenciadores de metadados** . Isso sincroniza os objetos entre o Gerenciador de metadados do Oracle e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Também contém comandos para mostrar e ocultar os painéis de **saída** e de **lista de erros** e um **layout** de opção para gerenciar os layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios e migrar objetos e dados. Também fornece acesso às caixas de diálogo **configurações globais** e **configurações do projeto** .|  
|**Testador**|Contém comandos para criar e trabalhar com casos de teste, repositório e sistema de gerenciamento de backup.|  
|**Ajuda**|Fornece acesso à ajuda do SSMA e à caixa de diálogo **sobre** .|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e painel de Lista de Erros  
O menu **Exibir** fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel saída mostra mensagens de status do SSMA durante a conversão de objetos, a sincronização de objetos e a migração de dados.  
  
-   O painel de Lista de Erros mostra mensagens de erro, aviso e informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte Também  
[Migrar dados do Oracle para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[Referência da interface do usuário &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
