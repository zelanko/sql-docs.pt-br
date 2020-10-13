---
description: Configurando opções de conversão e migração (AccessToSQL)
title: Configurando opções de conversão e migração (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cc9a5328095f2ef839eb0c9617798299e46371fd
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987677"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Configurando opções de conversão e migração (AccessToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam como os objetos são convertidos, como os dados são migrados e como os tipos de dados de origem são mapeados para os tipos de dados de destino. Antes de converter objetos ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure ou migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, verifique se as opções de configuração são apropriadas para o projeto.  
  
## <a name="configuration-options-and-modes"></a>Opções de configuração e modos  
O SSMA tem quatro conjuntos de parâmetros de configuração e quatro modos para definir essas configurações: padrão, otimista, completo e personalizado. O modo padrão é recomendado para a maioria dos usuários. Use o modo otimista para conversões simples. Use o modo completo se desejar ver todas as mensagens. No modo personalizado, você define as opções.  
  
As configurações são descritas na seção "referência da interface do usuário" desta documentação. Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os seguintes tópicos:  
  
-   [Configurações do projeto (conversão)](./project-settings-conversion-accesstosql.md)  
  
-   [Configurações do projeto (migração)](./project-settings-migration-accesstosql.md)  
  
-   [Configurações do projeto (GUI)](../sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configurações do projeto (mapeamento de tipo)](./project-settings-type-mapping-accesstosql.md)  
  
-   [Configurações do projeto (SQL Azure)](./project-settings-azure-sql-db-accesstosql.md)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode definir as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  No menu **ferramentas** , selecione **configurações de projeto padrão**.  
  
2.  Na caixa de diálogo **configurações de projeto padrão** , siga um destes procedimentos:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações devem ser exibidas/alteradas no menu suspenso **versão de destino de migração** , clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão ou migração ou SQL Azure**.  
  
        > [!NOTE]  
        > SQL Azure opção estará disponível na guia **geral** somente se o tipo de projeto criado for SQL Azure.  
  
    -   Para selecionar um modo predefinido, selecione **padrão**, **otimista**ou **completo** na caixa suspensa **modo** .  
  
    -   Para especificar um modo personalizado, selecione **personalizado** na caixa **modo** , selecione uma opção no painel esquerdo, clique na configuração ou no valor no painel direito e, em seguida, selecione ou insira a nova configuração ou valor.  
  
3.  Clique em **OK** para salvar as configurações.  
  
Você também pode personalizar as configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações do projeto atual**  
  
1.  No menu **ferramentas** , selecione **configurações do projeto**.  
  
2.  Na caixa de diálogo **configurações do projeto** , siga um destes procedimentos:  
  
    -   Para selecionar um modo predefinido, selecione **padrão**, **otimista**ou **completo** na caixa suspensa **modo** .  
  
    -   Para especificar um modo personalizado, selecione **personalizado** na caixa **modo** , selecione uma opção no painel esquerdo, clique na configuração ou no valor no painel direito e, em seguida, selecione ou insira a nova configuração ou valor.  
  
3.  Clique em **OK** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando tipos de dados de origem e de destino](mapping-source-and-target-data-types-accesstosql.md)  
  
-   Para personalizar o mapeamento de bancos de dados de origem e de destino, consulte [mapeando bancos de dados de origem e de destino](mapping-source-and-target-databases-accesstosql.md)  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure definições de objeto. Para obter mais informações, consulte [convertendo objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
