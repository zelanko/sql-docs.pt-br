---
title: Trabalhando com projetos do SSMA (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 854d604680082375bba1d7fe5cca77d264ea7c9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-ssma-projects-oracletosql"></a>Trabalhando com projetos do SSMA (OracleToSQL)
Para migrar bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você primeiro crie um projeto SSMA. O projeto é um arquivo que contém as seguintes informações:  
  
-   Metadados sobre os bancos de dados do Oracle que você deseja migrar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Metadados sobre a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que receberá os dados e os objetos migrados.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Informações de Conexão.  
  
-   Configurações de projeto.  
  
Quando você abre um projeto, ele é desconectado do Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Que lhe permite trabalhar offline. Para obter informações sobre reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectando ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisando parâmetros de projeto padrão  
O SSMA contém várias configurações de conversão e carregamento de objetos de banco de dados, migração de dados e sincronizando SSMA com Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. As configurações padrão são apropriadas para vários usuários. No entanto, antes de criar um novo projeto SSMA, você deve examinar as configurações. Se desejar, você pode alterar as configurações padrão que serão usadas para todos os seus projetos novos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, clique em **configurações de projeto padrão**.  
  
2.  Selecione o tipo de projeto em **versão de destino de migração** lista suspensa para quais configurações são necessárias para ser exibida ou alterada e clique **geral** guia.  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, revise e altere as configurações conforme necessário. Para obter mais informações sobre essas configurações, consulte [configurações de projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Repita as etapas 1 a 3 para as páginas de migração, sincronização, carregar objetos do sistema, GUI e mapeamento de tipo.  
  
    -   Para obter informações sobre as configurações de migração, consulte [configurações de projeto &#40;migração&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Para obter informações sobre as configurações de objeto de sistema, consulte [configurações de projeto&#40;objetos do sistema carregar&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Para obter informações sobre as configurações de sincronização para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [configurações de projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Para obter informações sobre configurações de interface gráfica do usuário, consulte [configurações de projeto &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Para obter informações sobre configurações de mapeamento de tipo de dados, consulte [configurações de projeto &#40;mapeamento de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Criar novos projetos  
Para migrar dados de bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve primeiro criar um projeto.  
  
**Para criar um projeto**  
  
1.  Sobre o **arquivo** menu, clique em **novo projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  No **nome** , digite um nome para seu projeto.  
  
3.  No **local** caixa, digite ou selecione uma pasta para o projeto e, em seguida, clique em **Okey**.  
  
4.  No **migração para** lista suspensa, selecione a versão de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usado para migração. As opções disponíveis são:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>Personalizando configurações de projeto  
Além de definir configurações de projeto padrão que se aplicam a todos os novos projetos do SSMA, você pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Quando você personalizar mapeamentos de tipo de dados entre bancos de dados de origem e de destino, você pode definir mapeamentos no projeto, no banco de dados ou no nível de objeto. Para obter mais informações, consulte [mapeamento Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salvar um projeto, o SSMA retém as configurações do projeto e, opcionalmente, os metadados do banco de dados, para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   Sobre o **arquivo** menu, clique em **Salvar projeto**.  
  
    Se os esquemas no projeto foram alteradas ou não tem sido convertidas, SSMA solicitará para carregar e salvar metadados. Carregar e salvar metadados permitirá trabalhar offline. Ele também permite enviar um arquivo de projeto completo para outras pessoas, como a equipe de suporte técnico. Se você for solicitado a salvar metadados, faça o seguinte:  
  
    1.  Para cada esquema que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar metadados ainda, não selecione todas as caixas de seleção.  
  
    2.  Clique o **salvar** botão.  
  
        O SSMA analisará os esquemas do Oracle e salve os metadados para o arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado da Oracle e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Que lhe permite trabalhar offline. Para atualizar os metadados, carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para migrar dados, você deve reconectar-se ao Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para abrir um projeto**  
  
1.  Use um dos procedimentos a seguir:  
  
    -   Sobre o **arquivo** , aponte para **projetos recentes**e, em seguida, clique no projeto que você deseja abrir.  
  
    -   Sobre o **arquivo** menu, selecione **Abrir projeto**, localize o arquivo de projeto .o2ssproj, selecione o arquivo e, em seguida, clique em **abrir**.  
  
2.  Para reconectar-se ao Oracle, no **arquivo** menu, clique em **reconectar-se ao Oracle**.  
  
3.  Para reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], no **arquivo** menu, clique em **reconectar-se ao SQL Server**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [se conectar ao banco de dados Oracle (OracleToSQL)](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados Oracle migrando para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Conectar-se ao banco de dados Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[Conectando ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
