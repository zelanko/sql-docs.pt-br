---
title: Trabalhando com projetos do SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7e1be086b891d6888c6509b15adc6664b3022978
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830124"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>Trabalhar com projetos do SSMA (SybaseToSQL)
Migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você primeiro crie um projeto do SSMA. O projeto é um arquivo que contém metadados sobre os bancos de dados do ASE que você deseja migrar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, metadados sobre a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure que receberá os dados, e os objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure informações de conexão e configurações do projeto.  
  
Quando você abre um projeto, ele é desconectado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure. Isso permite que você trabalhe offline. Você pode se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Para obter mais informações, consulte [conectando ao SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [conectar-se ao BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisar as configurações padrão de projeto  
O SSMA contém várias opções de conversão e carregar objetos de banco de dados, migração de dados e sincronizando SSMA com ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. As configurações padrão para essas opções são apropriadas para muitos usuários. No entanto, antes de criar um novo projeto SSMA, examine as opções e, se você quiser alterar os padrões que serão usados para todos os seus projetos novos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações do projeto padrão**.  
  
2.  Selecione o tipo de projeto no **versão de destino de migração** lista suspensa para as configurações que são necessárias para ser exibida ou alterada e clique **geral** guia.  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, revise as opções, alterar as opções conforme necessário. Para obter mais informações sobre essas opções, consulte [configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Repita as etapas 1 a 3 para as páginas de migração, SQL Azure, carregando objetos, GUI e mapeamento de tipo.  
  
    -   Para obter informações sobre opções de migração, consulte [configurações do projeto &#40;migração&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Para obter informações sobre opções de carregamento de objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [configurações do projeto &#40;sincronização&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Para obter mais informações sobre as opções de interface gráfica do usuário, consulte [configurações do projeto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Para obter mais informações sobre as configurações de mapeamento de tipo de dados, clique em [configurações do projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Para obter mais informações sobre as opções do SQL Azure, consulte [configurações do projeto &#40;SQL do Azure &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > As configurações do SQL Azure serão exibidas somente quando você seleciona **migração para o SQL Azure** durante a criação de um projeto.  
  
## <a name="creating-new-projects"></a>Criação de novos projetos  
Para migrar dados de bancos de dados do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você deve primeiro criar um projeto.  
  
**Para criar um projeto**  
  
1.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  No **nome** , digite um nome para seu projeto.  
  
3.  No **local** caixa, digite ou selecione uma pasta para o projeto.  
  
4.  No **migração à** lista suspensa, selecione a versão de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para a migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
E, em seguida, clique em **Okey**.  
  
## <a name="customizing-project-settings"></a>Personalizando configurações de projeto  
Além de definir configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [definir opções do projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Quando você personaliza os mapeamentos de tipo de dados entre bancos de dados de origem e destino, você pode definir mapeamentos no projeto, no banco de dados ou no nível do objeto. Para obter mais informações sobre o mapeamento de tipo, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salvar um projeto, o SSMA retém as configurações de projeto e, opcionalmente, os metadados do banco de dados, para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   Sobre o **arquivo** menu, selecione **Salvar projeto**.  
  
    Se os bancos de dados dentro do projeto foram alterados ou não foram convertidos, o SSMA solicitará que você salve os metadados para o projeto. Salvando metadados lhe permitirá trabalhar offline e para enviar um arquivo de projeto completo para outras pessoas, incluindo a equipe de suporte técnico. Se você for solicitado a salvar os metadados, faça o seguinte:  
  
    1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvando metadados pode levar vários minutos. Se você não quiser salvar os metadados no momento, não selecione as caixas de seleção.  
  
    2.  Clique o **salvar** botão.  
  
        O SSMA analisará os esquemas ASE do Sybase e salvar os metadados para o arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do ASE e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure. Isso permite que você trabalhe offline. Para atualizar os metadados, carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Para migrar dados, você deve se reconectar ao ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
**Para abrir um projeto**  
  
1.  Use um dos procedimentos a seguir:  
  
    -   Sobre o **arquivo** , aponte para **projetos recentes**e, em seguida, selecione o projeto que você deseja abrir.  
  
    -   Sobre o **arquivo** menu, selecione **Abrir projeto**, localize o arquivo de projeto .s2ssproj, selecione o arquivo e, em seguida, clique em **abrir**.  
  
2.  Para se reconectar à ASE, nos **arquivo** menu, selecione **reconectar-se ao Sybase**.  
  
3.  Para se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, sobre o **arquivo** menu, selecione **reconectar-se ao SQL Server** / **reconectar-se ao SQL Azure**.  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [conectar-se ao Sybase ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Conectar-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[Conectando ao SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Conectar-se ao banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
