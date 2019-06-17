---
title: Definir as opções de projeto (SybaseToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 08b1084f2f54a204f82bc0d1a0ee4096d207d835
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667424"
---
# <a name="setting-project-options-sybasetosql"></a>Definir opções do projeto (SybaseToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam a conversão do objeto, o carregamento do objeto, o SQL azure, interface do usuário e configurações de migração de dados. Antes de converter objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure ou migrar os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, verifique se as opções de configuração são adequadas para o projeto.  
  
O SSMA permite configurar opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você cria. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem cinco conjuntos de configurações do projeto:  
  
1.  Informações do projeto  
  
2.  Geral (conversão, migração e coleta de dados)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  Mapeamento de tipo  
  
Ele também tem quatro modos para definir essas configurações:  
  
1.  Padrão  
  
2.  Otimistas  
  
3.  Completo  
  
4.  Personalizar  
  
O modo padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe do Sybase Adaptive Server Enterprise (ASE) atual e é mais fácil de ler. No entanto, a manter a sintaxe atual pode não ser precisa. Se a sintaxe do ASE deve ser convertida para equivalentes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de SQL Azure, o modo completo executa uma conversão completa, mas o código resultante pode ser mais difícil de ler. No modo personalizado, você deve definir as opções.  
  
As configurações são descritas na seção de referência de Interface do usuário desta documentação. Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Configurações do projeto &#40;sincronização&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Configurações do projeto &#40;interface gráfica do usuário&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Configurações do projeto &#40;banco de dados SQL do Azure &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto criado por você.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações do projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada de **versão de destino de migração** soltar para baixo em geral na parte inferior do painel esquerdo e, em seguida, selecione conversão ou migração ou SQL Azure.  
  
    -   Para selecionar um modo predefinido, nos **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar configurações personalizadas, selecione ou insira as novas configurações ou valores.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações do projeto**.  
  
2.  No **configurações do projeto** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Para selecionar um modo predefinido, nos **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar um modo personalizado, na **modo** lista suspensa caixa, selecione **personalizado**, selecione uma opção no painel esquerdo, clique na configuração ou o valor no painel direito e, em seguida, selecione ou insira a nova configuração ou valor.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Se você quiser personalizado para o mapeamento de tipos de dados de origem e destino, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados do Sybase para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou definições de objeto do SQL Azure. Para obter mais informações, consulte [converter objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
