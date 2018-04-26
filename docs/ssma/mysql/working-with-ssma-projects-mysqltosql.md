---
title: Trabalhando com projetos do SSMA (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32018a99e3bd376aa5d80df2c24c27a1aa341ec9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="working-with-ssma-projects-mysqltosql"></a>Trabalhando com projetos do SSMA (MySQLToSQL)
Para migrar bancos de dados MySQL para o SQL Server ou SQL Azure, primeiro você deve criar um projeto SSMA. O projeto é um arquivo que contém as seguintes informações:  
  
-   Metadados sobre os bancos de dados MySQL que você deseja migrar para o SQL Server ou SQL Azure.  
  
-   Metadados sobre a instância de destino do SQL Server ou SQL Azure que receberá os dados e os objetos migrados.  
  
-   Informações de conexão do SQL Server ou SQL Azure.  
  
-   Configurações de projeto.  
  
Quando você abre um projeto, ele é desconectado do MySQL e SQL Server ou SQL Azure. Que lhe permite trabalhar offline. Para obter mais informações sobre reconectar-se ao SQL Server, consulte [conectando ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>Revisando parâmetros de projeto padrão  
O SSMA contém várias configurações para converter e carregamento de banco de dados, migração de dados e sincronizando SSMA com o MySQL e SQL Server ou SQL Azure. As configurações padrão são apropriadas para vários usuários. No entanto, antes de criar um novo projeto SSMA, você deve examinar as configurações. Se necessário, você pode alterar as configurações padrão que serão usadas para todos os seus projetos novos.  
  
##### <a name="to-review-default-project-settings"></a>Para examinar as configurações de projeto padrão  
  
1.  Selecione **configurações de projeto padrão** do **ferramentas** menu.  
  
2.  Selecione o tipo de projeto em **versão de destino de migração** lista suspensa para quais configurações devem ser exibidos / alterado e clique **geral** guia.  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, revise e altere as configurações conforme necessário. Para obter mais informações sobre essas configurações, consulte [configurações de projeto &#40;conversão&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  Repita as etapas 1 a 3 para as páginas de migração, sincronização, o SQL Azure, GUI e mapeamento de tipo.  
  
-   Para obter informações sobre as configurações de migração, consulte [configurações de projeto &#40;migração&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   Para obter informações sobre configurações de sincronização para o SQL Server, consulte [configurações de projeto &#40;sincronização&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   Para obter informações sobre configurações de interface gráfica do usuário, consulte [projeto configurações (GUI) (SSMA comum)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
-   Para obter informações sobre configurações de mapeamento de tipo de dados, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   Para obter informações sobre as configurações do SQL Azure, consulte [configurações de projeto &#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> As configurações do SQL Azure serão exibidas apenas quando você seleciona **migração para o SQL Azure** durante a criação de um projeto.  
  
## <a name="creating-new-projects"></a>Criar novos projetos  
Para migrar dados de bancos de dados MySQL para o SQL Server ou SQL Azure, você deve criar um projeto.  
  
##### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Selecione **novo projeto** do **arquivo** menu. A caixa de diálogo **Novo Projeto** será exibida. No menu **Arquivo**, selecione **Novo Projeto**. A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  No **nome** , digite um nome para seu projeto.  
  
3.  No **local** caixa, digite ou selecione uma pasta para o projeto.  
  
4.  No **migração para** lista suspensa, selecione a versão de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usado para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   Azure SQL DB  
  
E, em seguida, clique em **Okey**  
  
O SSMA cria o arquivo de projeto.  
  
## <a name="customizing-project-settings"></a>Personalizando configurações de projeto  
Além de definir o padrão configurações de projeto que se aplicam a todos os novos projetos do SSMA, você também podem personalizar as configurações para cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
Quando você personalizar mapeamentos de tipo de dados entre os bancos de dados de origem e de destino, você pode definir mapeamentos no projeto, no banco de dados ou no nível de objeto. Para obter mais informações, consulte [mapeamento MySQL e tipos de dados do SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
O recurso de salvar projetos permite ao usuário salvar essencialmente as configurações do projeto e, opcionalmente, os metadados do banco de dados para o arquivo de projeto SSMA.  
  
##### <a name="to-save-a-project"></a>Para salvar um projeto  
  
-   Sobre o **arquivo** menu, selecione **salvar** projeto.  
  
Se os bancos de dados dentro do projeto foram alteradas ou não tem sido convertidos, o SSMA solicitará que você carregar e salvar metadados. Carregar e salvar metadados permitem trabalhar offline. Ele também permite enviar um arquivo de projeto completo para outras pessoas, como a equipe de suporte técnico. Se você for solicitado a salvar metadados, faça o seguinte:  
  
1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados. Salvar metadados pode levar vários minutos. Se você não quiser salvar metadados neste momento, não selecione todas as caixas de seleção.  
  
2.  Clique em **Salvar**.  
  
O SSMA analisará os esquemas do MySQL e salve os metadados para o arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do MySQL e do SQL Server ou SQL Azure. Isso lhe permite trabalhar offline. Para atualizar os metadados, carregar objetos de banco de dados no SQL Server ou SQL Azure. Para migrar os dados, você deve reconectar-se ao SQL Server ou SQL Azure.  
  
##### <a name="to-open-a-project"></a>Para abrir um projeto  
  
1.  Use um dos procedimentos a seguir:  
  
    1.  Sobre o **arquivo** , aponte para **projetos recentes**.  
  
    2.  Selecione o projeto que você deseja abrir.  
  
    3.  Sobre o **arquivo** menu, selecione **Abrir projeto**, localize o arquivo de projeto .m2ssproj, selecione o arquivo e, em seguida, clique em **abrir**.  
  
2.  Para reconectar-se ao MySQL, no **arquivo** menu, selecione **reconectar ao MySQL**.  
  
3.  Para reconectar-se ao SQL Server, no **arquivo** menu, selecione **reconectar-se ao SQL Server**.  
  
4.  Para reconectar-se ao SQL Azure, no **arquivo** menu, selecione **reconectar-se ao SQL Azure.**  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [conectando ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Conectando ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Bancos de dados MySQL migrando para o SQL Server - banco de dados SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectando ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Conectar-se ao banco de dados SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
