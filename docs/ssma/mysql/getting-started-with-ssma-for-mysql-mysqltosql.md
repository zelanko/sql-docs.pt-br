---
title: Guia de Introdução com o SSMA para MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f7101f7c249b478524955b3d601a7b20bd178498
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Guia de Introdução com o SSMA para MySQL (MySQLToSQL)
Migration Assistant SSMA (SQL Server) para MySQL permite converter esquemas de banco de dados MySQL para esquemas SQL Server ou banco de dados do Azure SQL rapidamente, carregar os esquemas resultantes no SQL Server ou banco de dados de SQL do Azure e migrar dados do MySQL para o SQL Server ou banco de dados de SQL do Azure.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalando o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa de cliente SSMA em um computador que pode acessar o banco de dados do MySQL de origem e a instância de destino do SQL Server ou banco de dados de SQL do Azure. Em seguida, instale os provedores do MySQL (MySQL 5.1 Driver ODBC (confiável)) no computador que está executando o programa de cliente do SSMA. Para obter instruções de instalação, consulte [instalando SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Para iniciar o SSMA, clique em **iniciar**, aponte para **todos os programas**, aponte para **SQL Server Migration Assistant para MySQL**e, em seguida, clique em **SQL Server Migration Assistant para MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA para Interface do Usuário MySQL  
Depois que o SSMA é instalado e licenciado, você pode usar o SSMA para migrar bancos de dados MySQL para o SQL Server ou banco de dados do Azure SQL. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de iniciar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![SSMA para Interface gráfica do usuário do MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA para Interface gráfica do usuário do MySql")  
  
Para iniciar uma migração, você deve:  
  
1.  Crie um novo projeto.  
  
2.  Conecte-se ao banco de dados MySQL.  
  
3.  Após uma conexão bem-sucedida, os esquemas de MySQL aparecerá no Gerenciador de metadados do MySQL. Objetos com o botão direito no Gerenciador de metadados do MySQL para executar tarefas como criam relatórios que avaliam conversões para o banco de dados do SQL Server/Azure SQL.  
  
Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do SQL Server. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do SQL Server será exibida no Gerenciador de metadados do SQL Server. Depois de converter esquemas do MySQL para esquemas SQL Server, selecione os esquemas convertidos no Gerenciador de metadados do SQL Server e, em seguida, sincronizar os esquemas com o SQL Server.  
  
Você deve se conectar ao banco de dados de SQL Azure se você tiver selecionado o banco de dados do Azure SQL de migração para a lista suspensa na caixa de diálogo Novo projeto. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do banco de dados de SQL do Azure será exibido no Gerenciador de metadados de banco de dados de SQL do Azure. Depois de converter esquemas do MySQL para esquemas de banco de dados de SQL do Azure, selecione os esquemas convertidos no Gerenciador de metadados de banco de dados de SQL do Azure e, em seguida, sincronizar os esquemas com o banco de dados do Azure SQL.  
  
Depois de sincronizar convertidas esquemas com o SQL Server ou banco de dados de SQL do Azure, você pode retornar ao Gerenciador de metadados do MySQL e migrar dados de esquemas do MySQL para bancos de dados do SQL Server ou banco de dados de SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como executá-los, consulte [migração de bancos de dados MySQL para o SQL Server - Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
As seções a seguir descrevem os recursos da interface de usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações em bancos de dados do SQL Server e MySQL.  
  
### <a name="mysql-metadata-explorer"></a>Gerenciador de metadados do MySQL  
Gerenciador de metadados do MySQL mostra informações sobre esquemas de MySQL. Usando o Gerenciador de metadados do MySQL, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a sintaxe do SQL Server. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Selecionar tabelas para migração de dados e, em seguida, migrar os dados dessas tabelas para o SQL Server. Para obter mais informações, consulte [migrando dados do MySQL para o SQL Server - Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server ou o Gerenciador de metadados do banco de dados SQL do Azure  
SQL Server ou o Gerenciador de metadados de banco de dados de SQL Azure mostra informações sobre uma instância do SQL Server ou banco de dados de SQL do Azure. Quando você se conectar a uma instância do SQL Server ou banco de dados de SQL do Azure, SSMA recupera metadados sobre essa instância e as armazena no arquivo de projeto.  
  
Você pode usar esse gerenciador de metadados para selecionar objetos de banco de dados MySQL convertidos e, em seguida, sincronizar os objetos com a instância do SQL Server ou banco de dados de SQL do Azure.  
  
Para obter mais informações, consulte [sincronização (MySQL para o SQL Server / banco de dados de SQL Azure)](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do MySQL, guias de nove aparecerá: **tabela**, **SQL**, **mapeamento de tipo**, **dados**, **configurações**, **Charset mapeamento**, **modos SQL**, **propriedades**, e **relatório**. O **relatório** guia contém informações somente depois de criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela no Gerenciador de metadados do SQL Server, estas três guias aparecerá: **tabela**, **SQL** e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do MySQL, você pode alterar mapeamentos de tipos de mapeamento de conjunto de caracteres, modos de SQL. Para converter os mapeamentos de tipo alterado ou o mapeamento de conjunto de caracteres ou modos SQL, faça alterações antes de converter esquemas.  
  
-   No Gerenciador de metadados do SQL Server, você pode alterar as propriedades de tabela e índice na guia da tabela. Para ver as alterações no SQL Server, fazer essas alterações antes de carregar os esquemas no SQL Server.  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou de destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, conectando ao MySQL e se conectar ao SQL Server ou banco de dados de SQL do Azure. Esses botões lembram os comandos no **arquivo** menu.  
  
### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra a migração comandos da barra de ferramentas:  
  
|||  
|-|-|  
|**botão**|**Função**|  
|**Criar relatório**|Converte os objetos selecionados do MySQL para objetos do SQL Server ou banco de dados do Azure SQL e, em seguida, cria um relatório que mostra a conversão foi como bem-sucedida.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do MySQL.|  
|**Converter esquema**|Converte os objetos selecionados do MySQL em objetos do SQL Server ou banco de dados de SQL do Azure.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do MySQL.|  
|**Migrar dados**|Migra os dados do banco de dados MySQL para o SQL Server ou banco de dados de SQL do Azure. Antes de executar esse comando, converter os esquemas do MySQL para esquemas SQL Server ou banco de dados de SQL do Azure e, em seguida, carregue os objetos no SQL Server ou banco de dados de SQL do Azure.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do MySQL.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|||  
|-|-|  
|**Menu**|**Descrição**|  
|**Arquivo**|Contém comandos para trabalhar com projetos, conectando-se ao MySQL e no SQL Server ou banco de dados de SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes. Para abrir **gerenciar indicadores** caixa de diálogo, no menu Editar clique em Gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores. Você pode usar os botões à direita da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados de pesquisadores** comando. Que sincroniza os objetos entre o Gerenciador de metadados do MySQL e SQL Server ou do Gerenciador de metadados de banco de dados de SQL do Azure. Também contém comandos para mostrar e ocultar o **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar com os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, converter o esquema, de atualização do banco de dados, migrar objetos e dados e salve como Script. Também fornece acesso a **configurações globais, configurações de projeto padrão** e **configurações de projeto** caixas de diálogo.|  
|**Ajuda**|Fornece acesso para ajudar o SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra erro, aviso e mensagens informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface de usuário &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Migração de dados MySQL para o SQL Server - banco de dados SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
