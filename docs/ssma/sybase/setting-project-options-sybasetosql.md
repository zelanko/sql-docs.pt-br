---
title: "Definir as opções de projeto (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 40c2bffdb58fadfa3a9c7da58cf68b8c4390cd16
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-sybasetosql"></a>Definindo opções de projeto (SybaseToSQL)
Para cada projeto SSMA, você pode definir opções de nível de projeto. Essas opções especificam a conversão do objeto, o carregamento de objeto, do SQL azure, interface do usuário e configurações de migração de dados. Antes de converter objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure ou migrar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, verifique se as opções de configuração são adequadas para o projeto.  
  
O SSMA permite configurar as opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você criar. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem cinco conjuntos de configurações de projeto:  
  
1.  Informações do projeto  
  
2.  Geral (conversão, migração e coleta de dados)  
  
3.  Synchronization  
  
4.  INTERFACE GRÁFICA DO USUÁRIO  
  
5.  Mapeamento de tipo  
  
Ele também tem quatro modos para definir essas configurações:  
  
1.  Padrão  
  
2.  Otimistas  
  
3.  Completo  
  
4.  Personalizar  
  
O padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe do Sybase Adaptive Server Enterprise (ASE) atual e é mais fácil de ler. No entanto, a manter a sintaxe atual pode não ser precisa. Se a sintaxe ASE deve ser convertida ao equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure, o modo completo executará uma conversão completa, mas o código resultante pode ser mais difícil de ler. No modo personalizado, você deve definir as opções.  
  
As configurações são descritas na seção de referência de Interface de usuário desta documentação. Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações de projeto &#40; Conversão de &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Configurações de projeto &#40; Migração de &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Configurações de projeto &#40; Sincronização &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Configurações de projeto &#40; Interface gráfica do usuário &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configurações de projeto &#40; Mapeamento de tipo de &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Configurações de projeto &#40; Banco de dados SQL do Azure &#41; &#40; SybaseToSQL &#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Definindo opções de projeto  
Em SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações de projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** drop para baixo em geral na parte inferior do painel esquerdo e selecione conversão ou migração ou SQL Azure.  
  
    -   Para selecionar um modo predefinido, no **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar configurações personalizadas, selecione ou insira as configurações da nova ou valores.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações de projeto**.  
  
2.  No **configurações de projeto** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Para selecionar um modo predefinido, no **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar um modo personalizado, no **modo** menu suspenso Selecione **personalizado**, selecione uma opção no painel esquerdo, clique na configuração ou o valor no painel direito e, em seguida, selecione ou digite a nova configuração ou o valor.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Se você quiser personalizado para o mapeamento de tipos de dados de origem e de destino, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados Sybase em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de objeto do SQL Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

