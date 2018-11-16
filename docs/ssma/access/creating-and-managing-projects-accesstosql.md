---
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1cf23a076f7e4d7e873f48988364c51b1daa03b0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663375"
---
# <a name="creating-and-managing-projects-accesstosql"></a>Criando e gerenciando projetos (AccessToSQL)
Para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você deve primeiro criar um projeto do SSMA. O projeto é um arquivo que contém metadados sobre os bancos de dados de acesso que você deseja migrar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, metadados sobre a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure que receberá os dados, e os objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações de conexão e configurações do projeto.  
  
## <a name="reviewing-default-project-settings"></a>Revisar as configurações padrão de projeto  
O SSMA contém várias opções de conversão e a sincronização de objetos de banco de dados e para a conversão de dados. A configuração padrão para essas opções é apropriada para muitos usuários. No entanto, antes de criar um novo projeto SSMA, você deve revisar as opções e, se você quiser alterar as configurações padrão que serão usadas para todos os seus projetos novos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações do projeto padrão**.  
  
2.  Selecione o tipo de projeto no **versão de destino de migração** lista suspensa para quais configurações devem ser exibidos / alterado e clique **geral** guia.  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, revise as opções. Para obter mais informações sobre essas opções, consulte [configurações do projeto (conversão)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).  
  
5.  Altere as opções conforme necessário.  
  
6.  Repita as etapas anteriores para o **migração**, **GUI**, e **mapeamento de tipo** páginas.  
  
    -   Para obter informações sobre opções de migração, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
    -   Para obter informações sobre as opções de interface do usuário, consulte [configurações de projeto (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
    -   Para obter mais informações sobre as configurações de mapeamento de tipo de dados, consulte [configurações do projeto (mapeamento de tipo)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655).  
  
    -   Para obter informações sobre as configurações do SQL Azure, consulte [configurações do projeto (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e).  
  
**Observação** configurações do SQL Azure estará disponíveis somente quando você seleciona a migração para o SQL Azure durante a criação de um projeto.  
  
## <a name="creating-new-projects"></a>Criação de novos projetos  
O SSMA é iniciado sem carregar um projeto padrão. Para migrar dados de bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você deve criar um projeto.  
  
**Para criar um novo projeto**  
  
1.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  No **nome** , digite um nome para seu projeto.  
  
3.  No **local** caixa, digite ou selecione uma pasta do projeto  
  
4.  Na migração para o menu suspenso, selecione um do SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / 2016 / Azure SQL DB do SQL Server e, em seguida, clique em **Okey**.  
  
O SSMA cria o arquivo de projeto. Agora você pode executar a próxima etapa do [adicionando um ou mais bancos de dados do Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="customizing-project-settings"></a>Personalizando configurações de projeto  
Além de definir configurações de projeto padrão, que se aplicam a todos os novos projetos do SSMA, você também pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [conversão de configuração e opções de migração](setting-conversion-and-migration-options-accesstosql.md).  
  
Quando você personaliza os mapeamentos de tipo de dados entre bancos de dados de origem e destino, você pode definir mapeamentos no projeto, no banco de dados ou no nível do objeto. Para obter mais informações sobre o mapeamento de tipo, consulte [tipos de dados de destino e origem do mapeamento](mapping-source-and-target-data-types-accesstosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salvar um projeto, o SSMA persiste as configurações de projeto e, opcionalmente, os metadados do banco de dados, para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   Sobre o **arquivo** menu, selecione **Salvar projeto**.  
  
    Se os bancos de dados dentro do projeto foram alterados ou não foram convertidos, o SSMA solicitará que você salve os metadados para o projeto. Salvando metadados permite que você trabalhe offline. Ele também permite que você enviar um arquivo de projeto completo para outras pessoas, incluindo a equipe de suporte técnico. Se você for solicitado a salvar os metadados, faça o seguinte:  
  
    1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvando metadados pode levar vários minutos. Se você não quiser salvar os metadados no momento, não selecione as caixas de seleção.  
  
    2.  Clique em **Salvar**.  
  
        O SSMA analisará os esquemas de acesso e salvar os metadados para o arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure. Isso permite que você trabalhe offline. Para atualizar objetos de banco de dados de carregamento de metadados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Para migrar dados, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
**Para abrir um projeto**  
  
1.  Use um dos procedimentos a seguir:  
  
    -   Sobre o **arquivo** , aponte para **projetos recentes**e, em seguida, selecione o projeto que você deseja abrir.  
  
    -   Sobre o **arquivo** menu, selecione **Abrir projeto**, localize o arquivo de projeto .a2ssproj, selecione o arquivo e, em seguida, clique em **abrir**.  
  
2.  Para se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]diante a **arquivo** menu, selecione **reconectar-se ao SQL Server**.  
  
3.  Para reconectar-se ao SQL Azure, sobre o **arquivo** menu, selecione **reconectar-se ao SQL Azure.**  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no processo de migração [adicionar um ou mais bancos de dados do Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Adicionando e removendo arquivos de banco de dados do Access](adding-and-removing-access-database-files-accesstosql.md)  
  
