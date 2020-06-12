---
title: Introdução com o SSMA para MySQL (MySQLToSQL) | Microsoft Docs
description: Saiba mais sobre o processo de instalação do SSMA (Assistente de Migração do SQL Server) para MySQL e familiarize-se com a interface do usuário do SSMA.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a6dce90d0c8626032d92c9ecec61cbbaf2556e90
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293793"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Introdução ao SSMA para MySQL (MySQLToSQL)
O Assistente de Migração do SQL Server (SSMA) para MySQL permite converter rapidamente esquemas de banco de dados MySQL em esquemas de BD SQL Server ou SQL do Azure, carregar os esquemas resultantes em SQL Server ou BD SQL do Azure e migrar dados de MySQL para SQL Server ou BD SQL do Azure.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface do usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa cliente do SSMA em um computador que possa acessar o banco de dados MySQL de origem e a instância de destino do SQL Server ou do BD SQL do Azure. Em seguida, instale os provedores do MySQL (driver do MySQL ODBC 5,1 (confiável)) no computador que está executando o programa cliente do SSMA. Para obter instruções de instalação, consulte [instalando o SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Para iniciar o SSMA, clique em **Iniciar**, aponte para **todos os programas**, aponte para **Assistente de migração do SQL Server para MySQL**e clique em **Assistente de migração do SQL Server para MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA para Interface do Usuário MySQL  
Depois que o SSMA for instalado e licenciado, você poderá usar o SSMA para migrar bancos de dados MySQL para SQL Server ou BD SQL do Azure. Ele ajuda a se familiarizar com a interface do usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![SSMA para Interface Gráfica do Usuário MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA para Interface Gráfica do Usuário MySql")  
  
Para iniciar uma migração, você deve:  
  
1.  Criar um novo projeto.  
  
2.  Conecte-se a um banco de dados MySQL.  
  
3.  Após uma conexão bem-sucedida, os esquemas do MySQL serão exibidos no Gerenciador de metadados do MySQL. Clique com o botão direito do mouse em objetos no Gerenciador de metadados MySQL para executar tarefas como criar relatórios que avaliam conversões para SQL Server/banco de BD SQL do Azure.  
  
Você também pode executar essas tarefas usando as barras de ferramentas e menus.  
  
Você também deve se conectar a uma instância do SQL Server. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados SQL Server aparecerá no Gerenciador de metadados SQL Server. Depois de converter os esquemas do MySQL em esquemas de SQL Server, selecione os esquemas convertidos em SQL Server Gerenciador de metadados e sincronize os esquemas com SQL Server.  
  
Você deve se conectar ao banco de BD SQL do Azure se tiver selecionado BD SQL do Azure na caixa de diálogo migrar para dropdown no novo projeto. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do Azure SQL DB será exibida no Gerenciador de metadados do BD SQL do Azure. Depois de converter os esquemas do MySQL em esquemas de BD SQL do Azure, selecione os esquemas convertidos no Gerenciador de metadados do banco de BD SQL do Azure e sincronize os esquemas com o banco de BD SQL do Azure.  
  
Depois de sincronizar os esquemas convertidos com o SQL Server ou o banco de dados SQL do Azure, você pode retornar ao Gerenciador de metadados do MySQL e migrar dados de esquemas do MySQL para os bancos de dado do SQL Server ou do BD SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como executá-las, consulte [migrando bancos de dados MySQL para SQL Server-BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em bancos de dados MySQL e SQL Server.  
  
### <a name="mysql-metadata-explorer"></a>Gerenciador de metadados MySQL  
O Gerenciador de metadados do MySQL mostra informações sobre os esquemas do MySQL. Usando o Gerenciador de metadados do MySQL, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecione objetos para conversão e converta os objetos para SQL Server sintaxe. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Selecione tabelas para migração de dados e migre os dados dessas tabelas para SQL Server. Para obter mais informações, consulte [migrando dados do MySQL para o SQL Server-BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server ou o Gerenciador de metadados do BD SQL do Azure  
SQL Server ou o Gerenciador de metadados do banco de dados SQL do Azure mostra informações sobre uma instância do SQL Server ou do banco de dados SQL do Azure. Quando você se conecta a uma instância do SQL Server ou do BD SQL do Azure, o SSMA recupera os metadados sobre essa instância e os armazena no arquivo de projeto.  
  
Você pode usar esse Gerenciador de metadados para selecionar objetos de banco de dados MySQL convertidos e, em seguida, sincronizar esses objetos com a instância do SQL Server ou do BD SQL do Azure.  
  
Para obter mais informações, consulte [sincronização (MySQL para SQL Server/banco de dados SQL do Azure)](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados estão as guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do MySQL, nove guias serão exibidas: **tabela**, **SQL**, **mapeamento de tipo**, **dados**, **configurações**, mapeamento de conjunto de **caracteres**, **modos SQL**, **Propriedades**e **relatório**. A guia **relatório** contém informações somente depois que você cria um relatório que contém o objeto selecionado. Se você selecionar uma tabela no SQL Server Gerenciador de metadados, três guias serão exibidas: **tabela**, **SQL** e **dados**.  
  
A maioria das configurações de metadados é somente leitura. No entanto, você pode alterar os seguintes metadados:  
  
-   No Gerenciador de metadados do MySQL, você pode alterar mapeamentos de tipo, mapeamento de charset, modos SQL. Para converter os mapeamentos de tipo alterado ou o mapeamento de charset ou modos SQL, faça alterações antes de converter os esquemas.  
  
-   No SQL Server Gerenciador de metadados, você pode alterar as propriedades de tabela e índice na guia tabela. Para ver essas alterações no SQL Server, faça essas alterações antes de carregar os esquemas em SQL Server.  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas de projeto e uma barra de ferramentas de migração.  
  
### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, conectar-se ao MySQL e conectar-se ao SQL Server ou ao banco de BD SQL do Azure. Esses botões se assemelham aos comandos no menu **arquivo** .  
  
### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra os comandos da barra de ferramentas de migração:  
  
|||  
|-|-|  
|**Botão**|**Função**|  
|**Criar Relatório**|Converte os objetos MySQL selecionados em objetos SQL Server ou BD SQL do Azure e, em seguida, cria um relatório que mostra a êxito da conversão.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados do MySQL.|  
|**Converter esquema**|Converte os objetos MySQL selecionados em objetos SQL Server ou BD SQL do Azure.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados do MySQL.|  
|**Migrar dados**|Migra dados do banco de dados MySQL para o SQL Server ou o BD SQL do Azure. Antes de executar esse comando, você deve converter os esquemas do MySQL em esquemas de banco de SQL Server ou SQL do Azure e, em seguida, carregar os objetos em SQL Server ou no banco de BD SQL do Azure.<br /><br />Esse comando é desabilitado a menos que os objetos sejam selecionados no Gerenciador de metadados do MySQL.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|||  
|-|-|  
|**Menu**|**Descrição**|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectar-se ao MySQL e conectar-se ao SQL Server ou ao BD SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes. Para abrir a caixa de diálogo **gerenciar indicadores** , no menu Editar, clique em gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores existentes. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o comando **sincronizar gerenciadores de metadados** . Isso sincroniza os objetos entre o Gerenciador de metadados do MySQL e o SQL Server ou o Gerenciador de metadados do BD SQL do Azure. Também contém comandos para mostrar e ocultar os painéis de **saída** e de **lista de erros** e um **layout** de opção para gerenciar com os layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, converter o esquema, atualizar do banco de dados, migrar objetos e data e salvar como script. Também fornece acesso às caixas de diálogo **configurações globais, configurações de projeto padrão** e **configurações do projeto** .|  
|**Ajuda**|Fornece acesso à ajuda do SSMA e à caixa de diálogo **sobre** .|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e painel de Lista de Erros  
O menu **Exibir** fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel saída mostra mensagens de status do SSMA durante a conversão de objetos, a sincronização de objetos e a migração de dados.  
  
-   O painel de Lista de Erros mostra mensagens de erro, aviso e informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Migrando dados do MySQL para o SQL Server-BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
