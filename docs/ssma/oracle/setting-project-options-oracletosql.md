---
title: Configurando opções de projeto (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 6947a51b731b22b28ffbaa509f7cd38be5e7ebc5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266526"
---
# <a name="setting-project-options-oracletosql"></a>Definir opções do projeto (OracleToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam a conversão de objetos, o carregamento de objetos, a interface do usuário e as configurações de migração de dados. Antes de converter objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, verifique se as opções de configuração são apropriadas para o projeto.  
  
O SSMA permite que você configure opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você criar. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Opções de configuração e modos  
O SSMA tem cinco conjuntos de configurações de projeto:  
  
-   Informações do Projeto  
  
-   Geral (conversão, migração, carregamento de objetos)  
  
-   Synchronization  
  
-   GUI  
  
-   Mapeamento de tipo  
  
Ele também tem quatro modos para definir essas configurações:  
  
-   Padrão  
  
-   Otimistas  
  
-   Completo  
  
-   Personalizado  
  
O modo padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe atual do Oracle e é mais fácil de ler. No entanto, manter a sintaxe atual pode não ser precisa. Se a sintaxe do Oracle precisar ser convertida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em sintaxe equivalente, o modo completo executará a conversão mais completa, mas o código resultante poderá ser mais difícil de ler. No modo personalizado, você define as opções.  
  
Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os seguintes tópicos:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [Configurações do projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [Configurações do projeto &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode definir as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  No menu **ferramentas** , clique em **configurações de projeto padrão**.  
  
2.  Na caixa de diálogo **configurações padrão do projeto** , use um dos seguintes procedimentos:  
  
    -   Selecione o tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas na lista suspensa **versão de destino de migração** clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione conversão ou migração.  
  
    -   Para selecionar um modo predefinido, na caixa suspensa **modo** , selecione **padrão**, **otimista**ou **completo**.  
  
    -   Para especificar configurações personalizadas, selecione ou insira as novas configurações ou valores.  
  
3.  Clique em **OK** para salvar as configurações.  
  
Você também pode personalizar as configurações para o projeto atual. Essas configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações do projeto atual**  
  
1.  No menu **ferramentas** , clique em **configurações do projeto**.  
  
2.  Na caixa de diálogo **configurações do projeto** , use um dos seguintes procedimentos:  
  
    -   Para selecionar um modo predefinido, na caixa suspensa **modo** , selecione **padrão**, **otimista**ou **completo**.  
  
    -   Para especificar um modo personalizado, na caixa **modo** , selecione **personalizado**e, em seguida, selecione as configurações de projeto apropriadas.  
  
3.  Clique em **OK** para salvar as configurações.  
  
## <a name="next-steps"></a>Próximas etapas  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando os tipos de dados Oracle e SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Caso contrário, você pode converter as definições de objeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados Oracle em definições de objeto. Para obter mais informações, consulte [convertendo esquemas Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Mapeamento de tipos de dados Oracle e SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
