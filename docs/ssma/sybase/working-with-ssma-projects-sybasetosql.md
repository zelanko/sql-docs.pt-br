---
title: Trabalhando com projetos do SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 58b7ff093b11c844b295173b9be205443382edde
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-ssma-projects-sybasetosql"></a>Trabalhando com projetos do SSMA (SybaseToSQL)
Para migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você primeiro crie um projeto SSMA. O projeto é um arquivo que contém metadados sobre os bancos de dados ASE que você deseja migrar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, metadados sobre a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure que receberá os dados, e os objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou informações de conexão do SQL Azure e as configurações do projeto.  
  
Quando você abre um projeto, ele é desconectado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Isso lhe permite trabalhar offline. Você pode se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Para obter mais informações, consulte [conectando ao SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [se conectar ao banco de dados do Azure SQL &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisando parâmetros de projeto padrão  
O SSMA contém várias opções de conversão e carregamento de objetos de banco de dados, migração de dados e sincronizando SSMA com ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. As configurações padrão para essas opções são apropriadas para vários usuários. No entanto, antes de criar um novo projeto SSMA, examine as opções e, se você quiser alterar os padrões que serão usados para todos os seus projetos novos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações de projeto padrão**.  
  
2.  Selecione o tipo de projeto em **versão de destino de migração** lista suspensa para quais configurações são necessárias para ser exibida ou alterada e clique **geral** guia.  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, revise as opções, alterar as opções conforme necessário. Para obter mais informações sobre essas opções, consulte [configurações de projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Repita as etapas 1 a 3 para as páginas de migração do SQL Azure, carregando objetos, GUI e mapeamento de tipo.  
  
    -   Para obter informações sobre opções de migração, consulte [configurações de projeto &#40;migração&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Para obter informações sobre opções de carregamento de objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [configurações de projeto &#40;sincronização&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Para obter mais informações sobre as opções de interface gráfica do usuário, consulte [configurações de projeto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Para obter mais informações sobre configurações de mapeamento de tipo de dados, clique em [configurações de projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Para obter mais informações sobre as opções do SQL Azure, consulte [configurações de projeto &#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > As configurações do SQL Azure serão exibidas apenas quando você seleciona **migração para o SQL Azure** durante a criação de um projeto.  
  
## <a name="creating-new-projects"></a>Criar novos projetos  
Para migrar dados de bancos de dados ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve primeiro criar um projeto.  
  
**Para criar um projeto**  
  
1.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  No **nome** , digite um nome para seu projeto.  
  
3.  No **local** caixa, digite ou selecione uma pasta para o projeto.  
  
4.  No **migração para** lista suspensa, selecione a versão de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usado para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL DB  
  
E, em seguida, clique em **Okey**.  
  
## <a name="customizing-project-settings"></a>Personalizando configurações de projeto  
Além de definir configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Quando você personalizar mapeamentos de tipo de dados entre bancos de dados de origem e de destino, você pode definir mapeamentos no projeto, no banco de dados ou no nível de objeto. Para obter mais informações sobre o mapeamento de tipo, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salvar um projeto, o SSMA retém as configurações do projeto e, opcionalmente, os metadados do banco de dados, para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   Sobre o **arquivo** menu, selecione **Salvar projeto**.  
  
    Se bancos de dados dentro do projeto foram alteradas ou não tem sido convertidos, SSMA solicitará que você salve os metadados para o projeto. Salvar metadados permitirá trabalhar offline e envie um arquivo de projeto completo para outras pessoas, incluindo a equipe de suporte técnico. Se você for solicitado a salvar metadados, faça o seguinte:  
  
    1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar metadados neste momento, não selecione todas as caixas de seleção.  
  
    2.  Clique o **salvar** botão.  
  
        O SSMA analisará os esquemas do Sybase ASE e salve os metadados para o arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado da ASE e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Isso lhe permite trabalhar offline. Para atualizar os metadados, carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Para migrar os dados, você deve reconectar ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
**Para abrir um projeto**  
  
1.  Use um dos procedimentos a seguir:  
  
    -   Sobre o **arquivo** , aponte para **projetos recentes**e, em seguida, selecione o projeto que você deseja abrir.  
  
    -   Sobre o **arquivo** menu, selecione **Abrir projeto**, localize o arquivo de projeto .s2ssproj, selecione o arquivo e, em seguida, clique em **abrir**.  
  
2.  Para reconectar-se ao ASE, no **arquivo** menu, selecione **reconectar para Sybase**.  
  
3.  Para reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, no **arquivo** menu, selecione **reconectar-se ao SQL Server** / **reconectar-se ao SQL Azure**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [conectar para Sybase ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Conectar-se para Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[Conectando ao SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Conectar-se ao banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
