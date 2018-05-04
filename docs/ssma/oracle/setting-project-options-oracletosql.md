---
title: Definir as opções de projeto (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 7f75ca6a7b2f3ee8ae645c25e1135787e92e8a89
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setting-project-options-oracletosql"></a>Definindo opções de projeto (OracleToSQL)
Para cada projeto SSMA, você pode definir opções de nível de projeto. Essas opções especificam a conversão do objeto, o carregamento de objeto, configurações de migração de dados e a interface do usuário. Antes de converter objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou migrar dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], verifique se as opções de configuração são adequadas para o projeto.  
  
O SSMA permite configurar as opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você criar. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem cinco conjuntos de configurações de projeto:  
  
-   Informações do projeto  
  
-   Geral (conversão, migração, o carregamento de objetos)  
  
-   Synchronization  
  
-   INTERFACE GRÁFICA DO USUÁRIO  
  
-   Mapeamento de tipo  
  
Ele também tem quatro modos para definir essas configurações:  
  
-   Padrão  
  
-   Otimistas  
  
-   Completo  
  
-   Personalizar  
  
O padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe do Oracle atual e é mais fácil de ler. No entanto, a manter a sintaxe atual pode não ser precisa. Se a sintaxe do Oracle deve ser convertida ao equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe, o modo completo executa a conversão mais completa, mas o código resultante pode ser mais difícil de ler. No modo personalizado, você deve definir as opções.  
  
Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [Configurações do projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [Configurações do projeto &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>Definindo opções de projeto  
Em SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, clique em **configurações de projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** suspensa clique **geral** na parte inferior do painel esquerdo e selecione conversão ou migração.  
  
    -   Para selecionar um modo predefinido, no **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar configurações personalizadas, selecione ou insira as configurações da nova ou valores.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, clique em **configurações de projeto**.  
  
2.  No **configurações de projeto** caixa de diálogo, use um dos procedimentos a seguir:  
  
    -   Para selecionar um modo predefinido, no **modo** caixa de lista suspensa, selecione **padrão**, **Optimistic**, ou **completo**.  
  
    -   Para especificar um modo personalizado, no **modo** selecione **personalizado**e, em seguida, selecione as configurações apropriadas do projeto.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeamento Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definições de objeto. Para obter mais informações, consulte [convertendo esquemas de Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Mapeamento de Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
