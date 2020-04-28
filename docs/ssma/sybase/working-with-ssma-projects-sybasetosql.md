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
ms.openlocfilehash: eb6f035b4d597e2b648134c195b698554dc78e12
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68072474"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>Trabalhar com projetos do SSMA (SybaseToSQL)
Para migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou SQL Azure, você primeiro cria um projeto do SSMA. O projeto é um arquivo que contém metadados sobre os bancos de dados ASE que você deseja migrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, metadados sobre a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure que receberá os objetos e dados migrados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure informações de conexão e as configurações do projeto.  
  
Quando você abre um projeto, ele é desconectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do ou SQL Azure. Isso permite que você trabalhe offline. Você pode se reconectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao ou SQL Azure. Para obter mais informações, consulte [conectando-se a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  /  [conectar-se ao banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisando configurações de projeto padrão  
O SSMA contém várias opções para converter e carregar objetos de banco de dados, migrar e sincronizar o SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com ase e ou SQL Azure. As configurações padrão para essas opções são apropriadas para muitos usuários. No entanto, antes de criar um novo projeto do SSMA, você deve examinar as opções e, se desejar, alterar os padrões que serão usados para todos os seus novos projetos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  No menu **ferramentas** , selecione **configurações de projeto padrão**.  
  
2.  Selecione o menu suspenso tipo de projeto na **versão de destino de migração** para o qual as configurações devem ser exibidas ou alteradas e clique em guia **geral** .  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, examine as opções, alterando as opções conforme necessário. Para obter mais informações sobre essas opções, consulte [configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Repita as etapas de 1-3 para as páginas migração, SQL Azure, carregar objetos, GUI e mapeamento de tipo.  
  
    -   Para obter informações sobre opções de migração, consulte [configurações do projeto &#40;migração&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Para obter informações sobre as opções de carregamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de objetos no, consulte [configurações do projeto &#40;sincronização&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Para obter mais informações sobre opções de GUI, consulte [configurações de projeto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Para obter mais informações sobre configurações de mapeamento de tipo de dados, clique em [configurações do projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Para obter mais informações sobre opções de SQL Azure, consulte [configurações de projeto &#40;banco de dados SQL do Azure &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > As configurações de SQL Azure serão exibidas somente quando você selecionar **migração para SQL Azure** ao criar um projeto.  
  
## <a name="creating-new-projects"></a>Criando novos projetos  
Para migrar dados de bancos de dado ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou SQL Azure, você deve primeiro criar um projeto.  
  
**Para criar um projeto**  
  
1.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** aparecerá.  
  
2.  Na caixa **nome** , insira um nome para o seu projeto.  
  
3.  Na caixa **local** , insira ou selecione uma pasta para o projeto.  
  
4.  Na lista suspensa **migração para** , selecione a versão do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   BD SQL do Azure  
  
E clique em **OK**.  
  
## <a name="customizing-project-settings"></a>Personalizando as configurações do projeto  
Além de definir as configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Quando você personaliza mapeamentos de tipo de dados entre bancos de dado de origem e de destino, você pode definir mapeamentos no nível do projeto, banco de dados ou objeto. Para obter mais informações sobre mapeamento de tipo, consulte [mapeando Sybase ase e SQL Server tipos de dados &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salva um projeto, o SSMA retém as configurações do projeto e, opcionalmente, os metadados do banco de dados para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   No menu **arquivo** , selecione **salvar projeto**.  
  
    Se os bancos de dados no projeto tiverem sido alterados ou não tiverem sido convertidos, o SSMA solicitará que você salve os metadados no projeto. Salvar metadados permitirá que você trabalhe offline e envie um arquivo de projeto completo para outras pessoas, incluindo a equipe de suporte técnico. Se for solicitado que você salve os metadados, faça o seguinte:  
  
    1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar os metadados neste ponto, não marque nenhuma caixa de seleção.  
  
    2.  Clique no botão **Salvar** .  
  
        O SSMA analisará os esquemas de ASE do Sybase e salvará os metadados no arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de ou SQL Azure. Isso permite que você trabalhe offline. Para atualizar metadados, carregue objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no ou SQL Azure. Para migrar dados, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ase e ou SQL Azure.  
  
**Para abrir um projeto**  
  
1.  Use um dos seguintes procedimentos:  
  
    -   No menu **arquivo** , aponte para **projetos recentes**e selecione o projeto que você deseja abrir.  
  
    -   No menu **arquivo** , selecione **Abrir projeto**, localize o arquivo de projeto. s2ssproj, selecione o arquivo e clique em **abrir**.  
  
2.  Para reconectar-se ao ASE, no menu **arquivo** , selecione **reconectar-se ao Sybase**.  
  
3.  Para se reconectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao ou SQL Azure, no menu **arquivo** , selecione **reconectar-se a SQL Server** / **reconectar-se a SQL Azure**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [conectar-se ao Sybase ase](connecting-to-sybase-ase-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Conectando-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[Conectando-se ao SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Conectando-se ao BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
