---
description: Criando e gerenciando projetos (AccessToSQL)
title: Criando e gerenciando projetos (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: ee6cf3bea905b169503851efe375fd614c4589e9
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988192"
---
# <a name="creating-and-managing-projects-accesstosql"></a>Criando e gerenciando projetos (AccessToSQL)
Para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, você deve primeiro criar um projeto do SSMA. O projeto é um arquivo que contém metadados sobre os bancos de dados do Access para os quais você deseja migrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, metadados sobre a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure que receberá os objetos e dados migrados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as informações de conexão e as configurações do projeto.  
  
## <a name="reviewing-default-project-settings"></a>Revisando configurações de projeto padrão  
O SSMA contém várias opções para a conversão e a sincronização de objetos de banco de dados e para a conversão de dados. A configuração padrão para essas opções é apropriada para muitos usuários. No entanto, antes de criar um novo projeto do SSMA, você deve examinar as opções e, se desejar, alterar as configurações padrão que serão usadas para todos os seus novos projetos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  No menu **ferramentas** , selecione **configurações de projeto padrão**.  
  
2.  Selecione o menu suspenso tipo de projeto na **versão de destino de migração** para o qual as configurações devem ser exibidas/alteradas e clique em guia **geral** .  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, examine as opções. Para obter mais informações sobre essas opções, consulte [configurações do projeto (conversão)](./project-settings-conversion-accesstosql.md).  
  
5.  Altere as opções conforme necessário.  
  
6.  Repita as etapas anteriores para as páginas de **migração**, **GUI**e **mapeamento de tipo** .  
  
    -   Para obter informações sobre opções de migração, consulte [configurações do projeto (migração)](./project-settings-migration-accesstosql.md).  
  
    -   Para obter informações sobre as opções de interface do usuário, consulte [configurações do projeto (GUI)](../sybase/project-settings-gui-sybasetosql.md).  
  
    -   Para obter mais informações sobre configurações de mapeamento de tipo de dados, consulte [configurações do projeto (mapeamento de tipo)](./project-settings-type-mapping-accesstosql.md).  
  
    -   Para obter informações sobre configurações de SQL Azure, consulte [configurações de projeto (SQL Azure)](./project-settings-azure-sql-db-accesstosql.md).  
  
**Observação** SQL Azure configurações estarão disponíveis somente quando você selecionar migração para SQL Azure ao criar um projeto.  
  
## <a name="creating-new-projects"></a>Criando novos projetos  
O SSMA inicia sem carregar um projeto padrão. Para migrar dados do Access Database para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, você deve criar um projeto.  
  
**Para criar um novo projeto**  
  
1.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** aparecerá.  
  
2.  Na caixa **nome** , insira um nome para o seu projeto.  
  
3.  Na caixa **local** , insira ou selecione uma pasta para o projeto  
  
4.  Na lista suspensa migração para, selecione um dos SQL Server 2005/SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016/banco de dados SQL do Azure e clique em **OK**.  
  
O SSMA cria o arquivo de projeto. Agora você pode executar a próxima etapa de [Adicionar um ou mais bancos de dados do Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="customizing-project-settings"></a>Personalizando as configurações do projeto  
Além de definir as configurações de projeto padrão, que se aplicam a todos os novos projetos do SSMA, você também pode personalizar as configurações de cada projeto. Para obter mais informações, consulte [definindo opções de conversão e migração](setting-conversion-and-migration-options-accesstosql.md).  
  
Quando você personaliza mapeamentos de tipo de dados entre bancos de dado de origem e de destino, você pode definir mapeamentos no nível do projeto, banco de dados ou objeto. Para obter mais informações sobre mapeamento de tipo, consulte [mapeando tipos de dados de origem e de destino](mapping-source-and-target-data-types-accesstosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salva um projeto, o SSMA persiste as configurações do projeto e, opcionalmente, os metadados do banco de dados para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   No menu **arquivo** , selecione **salvar projeto**.  
  
    Se os bancos de dados no projeto tiverem sido alterados ou não tiverem sido convertidos, o SSMA solicitará que você salve os metadados no projeto. Salvar metadados permite que você trabalhe offline. Ele também permite que você envie um arquivo de projeto completo para outras pessoas, incluindo a equipe de suporte técnico. Se for solicitado que você salve os metadados, faça o seguinte:  
  
    1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar os metadados neste ponto, não marque nenhuma caixa de seleção.  
  
    2.  Clique em **Salvar**.  
  
        O SSMA analisará os esquemas de acesso e salvará os metadados no arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Isso permite que você trabalhe offline. Para atualizar os metadados carregar objetos de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Para migrar dados, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
**Para abrir um projeto**  
  
1.  Use um dos seguintes procedimentos:  
  
    -   No menu **arquivo** , aponte para **projetos recentes**e selecione o projeto que você deseja abrir.  
  
    -   No menu **arquivo** , selecione **Abrir projeto**, localize o arquivo de projeto. a2ssproj, selecione o arquivo e clique em **abrir**.  
  
2.  Para se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no menu **arquivo** , selecione **reconectar-se a SQL Server**.  
  
3.  Para se reconectar ao SQL Azure, no menu **arquivo** , selecione **reconectar-se a SQL Azure.**  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [Adicionar um ou mais bancos de dados do Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Adicionando e removendo arquivos de banco de dados do Access](adding-and-removing-access-database-files-accesstosql.md)  
