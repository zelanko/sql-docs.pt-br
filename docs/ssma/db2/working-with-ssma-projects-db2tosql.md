---
title: Trabalhando com projetos do SSMA (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bb652a1d3a0d9c5ee08a936e24e521948d264fa8
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823296"
---
# <a name="working-with-ssma-projects-db2tosql"></a>Trabalhando com projetos do SSMA (DB2ToSQL)
Para migrar bancos de dados DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você primeiro cria um projeto do SSMA. O projeto é um arquivo que contém as seguintes informações:  
  
-   Metadados sobre os bancos de dados DB2 para os quais você deseja migrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Os metadados sobre a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que receberão os objetos e dados migrados.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]informações de conexão.  
  
-   Configurações do projeto.  
  
Quando você abre um projeto, ele é desconectado do DB2 e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso permite que você trabalhe offline. Para obter informações sobre como se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [conectando-se a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisando configurações de projeto padrão  
O SSMA contém várias configurações para converter e carregar objetos de banco de dados, migrar e sincronizar o SSMA com o DB2 e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As configurações padrão são apropriadas para muitos usuários. No entanto, antes de criar um novo projeto do SSMA, você deve revisar as configurações. Se desejar, você poderá alterar as configurações padrão que serão usadas para todos os seus novos projetos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  No menu **ferramentas** , clique em **configurações de projeto padrão**.  
  
2.  Selecione o menu suspenso tipo de projeto na **versão de destino de migração** para o qual as configurações devem ser exibidas ou alteradas e clique em guia **geral** .  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, examine e altere as configurações conforme necessário. Para obter mais informações sobre essas configurações, consulte [configurações do projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
5.  Repita as etapas 1-3 para a migração, sincronização, carregamento de objetos do sistema, GUI e páginas de mapeamento de tipo.  
  
    -   Para obter informações sobre configurações de migração, consulte [configurações do projeto &#40;migração&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md).  
  
    -   Para obter informações sobre configurações de objeto do sistema, consulte [configurações do projeto&#40;carregar objetos do sistema&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md).  
  
    -   Para obter informações sobre as configurações de sincronização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [configurações do projeto&#40;sincronização&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
    -   Para obter informações sobre configurações de GUI, consulte [configurações de projeto &#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md).  
  
    -   Para obter informações sobre configurações de mapeamento de tipo de dados, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="creating-new-projects"></a>Criando novos projetos  
Para migrar dados de bancos de dado DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve primeiro criar um projeto.  
  
**Para criar um projeto**  
  
1.  No menu **Arquivo**, clique em **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** aparecerá.  
  
2.  Na caixa **nome** , insira um nome para o seu projeto.  
  
3.  Na caixa **local** , insira ou selecione uma pasta para o projeto e clique em **OK**.  
  
4.  Na lista suspensa **migração para** , selecione a versão do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Banco de dados SQL do Azure  
  
## <a name="customizing-project-settings"></a>Personalizando as configurações do projeto  
Além de definir as configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md) e seções relacionadas.  
  
Quando você personaliza mapeamentos de tipo de dados entre bancos de dado de origem e de destino, você pode definir mapeamentos no nível do projeto, banco de dados ou objeto. Para obter mais informações, consulte [mappinging DB2 and SQL Server Data Types &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salva um projeto, o SSMA retém as configurações do projeto e, opcionalmente, os metadados do banco de dados para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   No menu **arquivo** , clique em **salvar projeto**.  
  
    Se os esquemas no projeto tiverem sido alterados ou não tiverem sido convertidos, o SSMA solicitará que você carregue e salve os metadados. O carregamento e o salvamento de metadados permitirão que você trabalhe offline. Ele também permite que você envie um arquivo de projeto completo para outras pessoas, como a equipe de suporte técnico. Se for solicitado que você salve os metadados, faça o seguinte:  
  
    1.  Para cada esquema que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar os metadados ainda, não marque nenhuma caixa de seleção.  
  
    2.  Clique no botão **Salvar** .  
  
        O SSMA analisará os esquemas do DB2 e salvará os metadados no arquivo do projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do DB2 e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso permite que você trabalhe offline. Para atualizar metadados, carregue objetos de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para migrar dados, você deve se reconectar ao DB2 e ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Para abrir um projeto**  
  
1.  Use um dos seguintes procedimentos:  
  
    -   No menu **arquivo** , aponte para **projetos recentes**e clique no projeto que você deseja abrir.  
  
    -   No menu **arquivo** , selecione **Abrir projeto**, localize o arquivo de projeto. o2ssproj, selecione o arquivo e clique em **abrir**.  
  
2.  Para reconectar-se ao DB2, no menu **arquivo** , clique em **reconectar-se ao DB2**.  
  
3.  Para se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no menu **arquivo** , clique em **reconectar-se a SQL Server**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [conectar-se ao banco de dados DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
## <a name="see-also"></a>Consulte Também  
[Migrar bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[Conectando-se ao banco de dados DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[Conectando-se ao SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
