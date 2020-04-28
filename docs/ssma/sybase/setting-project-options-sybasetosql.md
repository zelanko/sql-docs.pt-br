---
title: Configurando opções de projeto (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2c8d074db2fc1e8a9d29ecf5fdc0405524e9bb1a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020923"
---
# <a name="setting-project-options-sybasetosql"></a>Definir opções do projeto (SybaseToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam a conversão de objetos, o carregamento de objetos, o SQL Azure, a interface do usuário e as configurações de migração de dados. Antes de converter objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure ou migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, verifique se as opções de configuração são apropriadas para o projeto.  
  
O SSMA permite que você configure opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você criar. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Opções de configuração e modos  
O SSMA tem cinco conjuntos de configurações de projeto:  
  
1.  Informações do Projeto  
  
2.  Geral (conversão, migração e coleta de dados)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  Mapeamento de tipo  
  
Ele também tem quatro modos para definir essas configurações:  
  
1.  Padrão  
  
2.  Otimistas  
  
3.  Completo  
  
4.  Personalizado  
  
O modo padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe atual do Sybase Adaptive Server Enterprise (ASE) e é mais fácil de ler. No entanto, manter a sintaxe atual pode não ser precisa. Se a sintaxe do ASE precisar ser convertida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sintaxe equivalente ou SQL Azure, o modo completo executará uma conversão completa, mas o código resultante poderá ser mais difícil de ler. No modo personalizado, você define as opções.  
  
As configurações são descritas na seção referência da interface do usuário desta documentação. Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os seguintes tópicos:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Configurações do projeto &#40;sincronização&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Configurações do projeto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Configurações do projeto &#40;BD SQL do Azure &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode definir as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  No menu **ferramentas** , selecione **configurações de projeto padrão**.  
  
2.  Na caixa de diálogo **configurações padrão do projeto** , use um dos seguintes procedimentos:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas na lista suspensa **versão de destino de migração** clique em geral na parte inferior do painel esquerdo e, em seguida, selecione conversão ou migração ou SQL Azure.  
  
    -   Para selecionar um modo predefinido, na caixa suspensa **modo** , selecione **padrão**, **otimista**ou **completo**.  
  
    -   Para especificar configurações personalizadas, basta selecionar ou inserir as novas configurações ou valores.  
  
3.  Clique em **OK** para salvar as configurações.  
  
Você também pode personalizar as configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações do projeto atual**  
  
1.  No menu **ferramentas** , selecione **configurações do projeto**.  
  
2.  Na caixa de diálogo **configurações do projeto** , use um dos seguintes procedimentos:  
  
    -   Para selecionar um modo predefinido, na caixa suspensa **modo** , selecione **padrão**, **otimista**ou **completo**.  
  
    -   Para especificar um modo personalizado, na caixa suspensa **modo** , selecione **personalizado**, selecione uma opção no painel esquerdo, clique na configuração ou no valor no painel direito e, em seguida, selecione ou insira a nova configuração ou valor.  
  
3.  Clique em **OK** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Se você quiser personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando os tipos de dados do Sybase ase e SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Caso contrário, você pode converter as definições de objeto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados Sybase em ou SQL Azure definições de objeto. Para obter mais informações, consulte [convertendo objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
