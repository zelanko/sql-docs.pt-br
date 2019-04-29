---
title: Introdução ao SSMA para MySQL (MySQLToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1ae91f90bf601e4ef17ae2f363260dbb47a2822e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187139"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Introdução ao SSMA para MySQL (MySQLToSQL)
SQL Server SSMA (Migration Assistant) para MySQL permite converter esquemas de banco de dados MySQL para esquemas SQL Server ou SQL do Azure, carregar os esquemas resultantes no SQL Server ou o Azure SQL DB e migrar dados do MySQL para o SQL Server ou SQL do Azure rapidamente.  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, primeiro você deve instalar o programa cliente SSMA em um computador que pode acessar o banco de dados do MySQL de origem e a instância de destino do SQL Server ou SQL do Azure. Em seguida, instale os provedores de MySQL (Driver ODBC do MySQL 5.1 (confiável)) no computador que está executando o programa de cliente do SSMA. Para obter instruções de instalação, consulte [instalar o SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Para iniciar o SSMA, clique em **inicie**, aponte para **todos os programas**, aponte para **SQL Server Migration Assistant for MySQL**e, em seguida, clique em **migração do SQL Server Assistant for MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA para Interface do Usuário MySQL  
Depois que o SSMA é instalado e licenciado, você pode usar o SSMA para migrar bancos de dados MySQL para o SQL Server ou SQL do Azure. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![SSMA para Interface gráfica do usuário do MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA para Interface gráfica do usuário do MySql")  
  
Para iniciar uma migração, faça o seguinte:  
  
1.  Crie um novo projeto.  
  
2.  Conecte-se ao banco de dados MySQL.  
  
3.  Após uma conexão bem-sucedida, os esquemas de MySQL serão exibido no Gerenciador de metadados do MySQL. Objetos de botão direito do mouse no Gerenciador de metadados do MySQL para executar tarefas como criar relatórios que avaliam as conversões para o banco de dados do SQL Server/Azure SQL.  
  
Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do SQL Server. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados do SQL Server será exibido no Gerenciador de metadados do SQL Server. Depois de converter esquemas do MySQL para esquemas SQL Server, selecione esses esquemas convertidas no Gerenciador de metadados do SQL Server e, em seguida, sincronizar os esquemas com o SQL Server.  
  
Você deve conectar-se ao BD SQL do Azure se você tiver selecionado o BD SQL do Azure da migração para a lista suspensa na caixa de diálogo Novo projeto. Após uma conexão bem-sucedida, uma hierarquia de bancos de dados SQL do Azure aparecerá no Gerenciador de metadados de banco de dados de SQL do Azure. Depois de converter esquemas do MySQL para esquemas de BD SQL do Azure, selecione esses esquemas convertidas no Gerenciador de metadados de banco de dados de SQL do Azure e, em seguida, sincronizar os esquemas com o Azure SQL DB.  
  
Depois de sincronizar convertidas esquemas com o SQL Server ou SQL do Azure, você pode retornar ao Gerenciador de metadados do MySQL e migrar dados de esquemas do MySQL em bancos de dados do SQL Server ou SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como realizá-las, consulte [migração de bancos de dados MySQL para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Metadata Explorers  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações nos bancos de dados MySQL e SQL Server.  
  
### <a name="mysql-metadata-explorer"></a>Gerenciador de metadados do MySQL  
Gerenciador de metadados de MySQL mostra informações sobre esquemas de MySQL. Usando o Gerenciador de metadados do MySQL, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a sintaxe do SQL Server. Para obter mais informações, consulte [conversão de bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Selecionar tabelas para migração de dados e, em seguida, migrar os dados dessas tabelas para o SQL Server. Para obter mais informações, consulte [migrando dados do MySQL para o SQL Server – BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server ou do Gerenciador de metadados do banco de dados SQL do Azure  
SQL Server ou do Gerenciador de metadados de banco de dados de SQL do Azure mostra informações sobre uma instância do SQL Server ou SQL do Azure. Quando você se conecta a uma instância do SQL Server ou SQL do Azure, o SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar esse gerenciador de metadados para selecionar objetos de banco de dados MySQL convertidos e, em seguida, sincronizar esses objetos com a instância do SQL Server ou SQL do Azure.  
  
Para obter mais informações, consulte [sincronização (MySQL para o SQL Server / Azure SQL DB)](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do MySQL, guias de nove serão exibida: **Tabela**, **SQL**, **mapeamento de tipo**, **dados**, **configurações**, **Charset mapeamento**, **Modos SQL**, **Properties**, e **relatório**. O **relatório** guia contém informações somente depois de criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela no Gerenciador de metadados do SQL Server, as três guias serão exibidas: **Tabela**, **SQL** e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do MySQL, você pode alterar os mapeamentos de tipos de mapeamento de conjunto de caracteres, modos de SQL. Para converter os mapeamentos de tipo alterado ou o mapeamento de conjunto de caracteres ou modos SQL, faça as alterações antes de converter esquemas.  
  
-   No Gerenciador de metadados do SQL Server, você pode alterar as propriedades de tabela e índice na guia da tabela. Para ver essas alterações no SQL Server, faça essas alterações antes de carregar os esquemas no SQL Server.  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
A barra de ferramentas do projeto contém botões para trabalhar com projetos, conectar-se ao MySQL e conectar-se ao SQL Server ou SQL do Azure. Esses botões se parecer com os comandos na **arquivo** menu.  
  
### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra a migração de comandos da barra de ferramentas:  
  
|||  
|-|-|  
|**Button**|**Função**|  
|**Criar relatório**|Converte os objetos selecionados do MySQL em objetos do SQL Server ou SQL do Azure e, em seguida, cria um relatório que mostra a conversão foi bem-sucedida como.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do MySQL.|  
|**Converter esquema**|Converte os objetos selecionados do MySQL em objetos do SQL Server ou SQL do Azure.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do MySQL.|  
|**Migrar dados**|Migra dados do banco de dados MySQL para o SQL Server ou SQL do Azure. Antes de executar esse comando, você deve converter os esquemas do MySQL para esquemas SQL Server ou SQL do Azure e, em seguida, carregar os objetos no SQL Server ou SQL do Azure.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do MySQL.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|||  
|-|-|  
|**Menu**|**Descrição**|  
|**File**|Contém comandos para trabalhar com projetos, conectar-se ao MySQL e conectar-se ao SQL Server ou SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes. Para abrir **gerenciar indicadores** caixa de diálogo, no menu Editar clique em Gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores atuais. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados Explorers** comando. Que sincroniza os objetos entre o Gerenciador de metadados do MySQL e SQL Server ou o Gerenciador de metadados do Azure SQL DB. Também contém comandos para mostrar e ocultar os **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar com os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, converter o esquema, de atualização do banco de dados, migrar objetos e dados e salvar como Script. Também fornece acesso para o **configurações globais, configurações do projeto padrão** e **configurações do projeto** caixas de diálogo.|  
|**Ajuda**|Fornece acesso para ajudar a SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra o erro, aviso e mensagens informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface do usuário &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Migrar dados do MySQL para o SQL Server – BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
