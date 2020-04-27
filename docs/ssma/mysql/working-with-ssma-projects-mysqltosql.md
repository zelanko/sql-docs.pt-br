---
title: Trabalhando com projetos do SSMA (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 37a763c0acca891d8bbbc1a310edcb6f8b987436
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67904898"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>Trabalhar com projetos do SSMA (MySQLToSQL)
Para migrar bancos de dados MySQL para SQL Server ou SQL Azure, você deve primeiro criar um projeto do SSMA. O projeto é um arquivo que contém as seguintes informações:  
  
-   Metadados sobre os bancos de dados MySQL que você deseja migrar para SQL Server ou SQL Azure.  
  
-   Metadados sobre a instância de destino do SQL Server ou SQL Azure que receberá os objetos e dados migrados.  
  
-   SQL Server ou SQL Azure informações de conexão.  
  
-   Configurações do projeto.  
  
Quando você abre um projeto, ele é desconectado do MySQL e SQL Server ou SQL Azure. Isso permite que você trabalhe offline. Para obter mais informações sobre como reconectar-se ao SQL Server, consulte [conectando-se ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>Revisando configurações de projeto padrão  
O SSMA contém várias configurações para a conversão e o carregamento de banco de dados, a migração e a sincronização do SSMA com MySQL e SQL Server ou SQL Azure. As configurações padrão são apropriadas para muitos usuários. No entanto, antes de criar um novo projeto do SSMA, você deve revisar as configurações. Se necessário, você pode alterar as configurações padrão que serão usadas para todos os seus novos projetos.  
  
##### <a name="to-review-default-project-settings"></a>Para examinar as configurações de projeto padrão  
  
1.  Selecione **configurações de projeto padrão** no menu **ferramentas** .  
  
2.  Selecione o menu suspenso tipo de projeto na **versão de destino de migração** para o qual as configurações devem ser exibidas/alteradas e clique em guia **geral** .  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, examine e altere as configurações conforme necessário. Para obter mais informações sobre essas configurações, consulte [configurações do projeto &#40;conversão&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  Repita as etapas de 1-3 para as páginas de migração, sincronização, SQL Azure, GUI e mapeamento de tipo.  
  
-   Para obter informações sobre configurações de migração, consulte [configurações do projeto &#40;migração&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   Para obter informações sobre as configurações de sincronização para SQL Server, consulte [configurações do projeto &#40;sincronização&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   Para obter informações sobre configurações de GUI, consulte [configurações de projeto (GUI) (SSMA Common)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
-   Para obter informações sobre configurações de mapeamento de tipo de dados, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   Para obter informações sobre configurações de SQL Azure, consulte [configurações de projeto &#40;banco de dados SQL do Azure&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> As configurações de SQL Azure serão exibidas somente quando você selecionar **migração para SQL Azure** ao criar um projeto.  
  
## <a name="creating-new-projects"></a>Criando novos projetos  
Para migrar dados do MySQL para SQL Server ou SQL Azure, você deve criar um projeto.  
  
##### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Selecione **novo projeto** no menu **arquivo** . A caixa de diálogo **Novo Projeto** aparecerá. No menu **Arquivo**, selecione **Novo Projeto**. A caixa de diálogo **Novo Projeto** aparecerá.  
  
2.  Na caixa **nome** , insira um nome para o seu projeto.  
  
3.  Na caixa **local** , insira ou selecione uma pasta para o projeto.  
  
4.  Na lista suspensa **migração para** , selecione a versão do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   BD SQL do Azure  
  
E clique em **OK**  
  
O SSMA cria o arquivo de projeto.  
  
## <a name="customizing-project-settings"></a>Personalizando as configurações do projeto  
Além de definir as configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você também pode personalizar as configurações de cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
Ao personalizar os mapeamentos de tipo de dados entre os bancos de dado de origem e de destino, você pode definir mapeamentos no nível do projeto, do banco de dados ou do objeto. Para obter mais informações, consulte [mapeando MySQL e SQL Server tipos de dados &#40;&#41;MySQLToSQL ](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
O recurso salvar projetos permite que o usuário salve basicamente as configurações do projeto e, opcionalmente, os metadados do banco de dados para o arquivo de projeto do SSMA.  
  
##### <a name="to-save-a-project"></a>Para salvar um projeto  
  
-   No menu **arquivo** , selecione **salvar** projeto.  
  
Se os bancos de dados no projeto tiverem sido alterados ou não tiverem sido convertidos, o SSMA solicitará que você carregue e salve os metadados. Carregar e salvar metadados permite que você trabalhe offline. Ele também permite que você envie um arquivo de projeto completo para outras pessoas, como a equipe de suporte técnico. Se for solicitado que você salve os metadados, faça o seguinte:  
  
1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados. Salvar metadados pode levar vários minutos. Se você não quiser salvar os metadados neste ponto, não marque nenhuma caixa de seleção.  
  
2.  Clique em **Salvar**.  
  
O SSMA analisará os esquemas do MySQL e salvará os metadados no arquivo do projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do MySQL e de SQL Server ou SQL Azure. Isso permite que você trabalhe offline. Para atualizar metadados, carregue objetos de banco de dados em SQL Server ou SQL Azure. Para migrar dados, você deve se reconectar a SQL Server ou SQL Azure.  
  
##### <a name="to-open-a-project"></a>Para abrir um projeto  
  
1.  Use um dos seguintes procedimentos:  
  
    1.  No menu **arquivo** , aponte para **projetos recentes**.  
  
    2.  Selecione o projeto que você deseja abrir.  
  
    3.  No menu **arquivo** , selecione **Abrir projeto**, localize o arquivo de projeto. m2ssproj, selecione o arquivo e clique em **abrir**.  
  
2.  Para reconectar-se ao MySQL, no menu **arquivo** , selecione **reconectar-se ao MySQL**.  
  
3.  Para se reconectar ao SQL Server, no menu **arquivo** , selecione **reconectar-se a SQL Server**.  
  
4.  Para se reconectar ao SQL Azure, no menu **arquivo** , selecione **reconectar-se a SQL Azure.**  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [conectar-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectando-se ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Conectando-se ao BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
