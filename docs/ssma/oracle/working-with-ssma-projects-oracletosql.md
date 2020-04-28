---
title: Trabalhando com projetos do SSMA (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: b96aba990231225516a7ba8ccf1523b91cb56c86
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266356"
---
# <a name="working-with-ssma-projects-oracletosql"></a>Trabalhar com projetos do SSMA (OracleToSQL)
Para migrar bancos de dados Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para o, você primeiro cria um projeto do SSMA. O projeto é um arquivo que contém as seguintes informações:  
  
-   Metadados sobre os bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os quais você deseja migrar.  
  
-   Os metadados sobre a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino do que receberão os objetos e dados migrados.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]informações de conexão.  
  
-   Configurações do projeto.  
  
Quando você abre um projeto, ele é desconectado do Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e do. Isso permite que você trabalhe offline. Para obter informações sobre como se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [conectando-se a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisando configurações de projeto padrão  
O SSMA contém várias configurações para converter e carregar objetos de banco de dados, migrar e sincronizar o SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com o Oracle e o. As configurações padrão são apropriadas para muitos usuários. No entanto, antes de criar um novo projeto do SSMA, você deve revisar as configurações. Se desejar, você poderá alterar as configurações padrão que serão usadas para todos os seus novos projetos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  No menu **ferramentas** , clique em **configurações de projeto padrão**.  
  
2.  Selecione o menu suspenso tipo de projeto na **versão de destino de migração** para o qual as configurações devem ser exibidas ou alteradas e clique em guia **geral** .  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, examine e altere as configurações conforme necessário. Para obter mais informações sobre essas configurações, consulte [configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Repita as etapas 1-3 para a migração, sincronização, carregamento de objetos do sistema, GUI e páginas de mapeamento de tipo.  
  
    -   Para obter informações sobre configurações de migração, consulte [configurações do projeto &#40;migração&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Para obter informações sobre configurações de objeto do sistema, consulte [configurações do projeto&#40;carregar objetos do sistema&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Para obter informações sobre as configurações de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sincronização para o, consulte [configurações do projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Para obter informações sobre configurações de GUI, consulte [configurações de projeto &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Para obter informações sobre configurações de mapeamento de tipo de dados, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Criando novos projetos  
Para migrar dados de bancos de dados Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para o, você deve primeiro criar um projeto.  
  
**Para criar um projeto**  
  
1.  No menu **Arquivo**, clique em **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** aparecerá.  
  
2.  Na caixa **nome** , insira um nome para o seu projeto.  
  
3.  Na caixa **local** , insira ou selecione uma pasta para o projeto e clique em **OK**.  
  
4.  Na lista suspensa **migração para** , selecione a versão do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   BD SQL do Azure  
  
## <a name="customizing-project-settings"></a>Personalizando as configurações do projeto  
Além de definir as configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Quando você personaliza mapeamentos de tipo de dados entre bancos de dado de origem e de destino, você pode definir mapeamentos no nível do projeto, banco de dados ou objeto. Para obter mais informações, consulte [mapeando os tipos de dados Oracle e SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salva um projeto, o SSMA retém as configurações do projeto e, opcionalmente, os metadados do banco de dados para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   No menu **arquivo** , clique em **salvar projeto**.  
  
    Se os esquemas no projeto tiverem sido alterados ou não tiverem sido convertidos, o SSMA solicitará que você carregue e salve os metadados. O carregamento e o salvamento de metadados permitirão que você trabalhe offline. Ele também permite que você envie um arquivo de projeto completo para outras pessoas, como a equipe de suporte técnico. Se for solicitado que você salve os metadados, faça o seguinte:  
  
    1.  Para cada esquema que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar os metadados ainda, não marque nenhuma caixa de seleção.  
  
    2.  Clique no botão **Salvar** .  
  
        O SSMA analisará os esquemas Oracle e salvará os metadados no arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Isso permite que você trabalhe offline. Para atualizar metadados, carregue objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de dados no. Para migrar dados, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle e ao.  
  
**Para abrir um projeto**  
  
1.  Use um dos seguintes procedimentos:  
  
    -   No menu **arquivo** , aponte para **projetos recentes**e clique no projeto que você deseja abrir.  
  
    -   No menu **arquivo** , selecione **Abrir projeto**, localize o arquivo de projeto. o2ssproj, selecione o arquivo e clique em **abrir**.  
  
2.  Para se reconectar ao Oracle, no menu **arquivo** , clique em **reconectar-se ao Oracle**.  
  
3.  Para se reconectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ao, no menu **arquivo** , clique em **reconectar-se a SQL Server**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [conectar-se ao Oracle Database (OracleToSQL)](https://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Conectando-se ao Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[Conectando-se ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
