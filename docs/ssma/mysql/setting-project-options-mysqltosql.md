---
description: Definir opções do projeto (MySQLToSQL)
title: Configurando opções de projeto (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: df2a29b2d411c2502573ede95feefe9c1e061c5b
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987892"
---
# <a name="setting-project-options-mysqltosql"></a>Definir opções do projeto (MySQLToSQL)
Para cada projeto do SSMA, você pode definir opções de nível de projeto. Essas opções especificam como os objetos são convertidos, como os dados são migrados e como os tipos de dados de origem são mapeados para os tipos de dados de destino.  Antes de converter objetos para SQL Server ou SQL Azure ou migrar dados para SQL Server ou SQL Azure, verifique se as opções de configuração são apropriadas para o projeto.  
  
O SSMA permite que você configure as opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você criar. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Opções de configuração e modos  
O SSMA tem cinco conjuntos de configurações de projeto:  
  
-   Informações do Projeto  
  
-   Geral (conversão, migração e SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   Mapeamento de tipo  
  
As configurações do projeto podem ser definidas de quatro maneiras:  
  
-   Padrão  
  
-   Otimistas  
  
-   Completo  
  
-   Personalizado  
  
O modo padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe do MySQL atual e é mais fácil de ler. No entanto, manter a sintaxe atual pode não ser precisa. Se a sintaxe do MySQL precisar ser convertida em SQL Server equivalente ou sintaxe de SQL Azure, o modo completo executará a conversão mais completa. O código resultante, no entanto, pode ser mais difícil de ler. No modo personalizado, você pode definir as opções.  
  
Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os seguintes tópicos:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [Configurações do projeto (GUI) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [Configurações do projeto &#40;sincronização&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [Configurações do projeto &#40;banco de dados SQL do Azure&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>Definir opções do projeto  
No SSMA, você pode definir as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  No menu **ferramentas** , clique em **configurações de projeto padrão**.  
  
2.  Na caixa de diálogo **configurações padrão do projeto** , use um dos seguintes procedimentos:  
  
    1.  Selecione o tipo de projeto de migração para o qual as configurações devem ser exibidas/alteradas no menu suspenso **versão de destino de migração** , clique em **geral** na parte inferior do painel esquerdo e selecione opção de **conversão ou migração ou SQL Azure** .  
  
    2.  Para selecionar um modo predefinido, selecione **padrão**, **otimista**ou **completo** na caixa suspensa **modo** .  
  
    3.  Para especificar configurações personalizadas, selecione ou insira as novas configurações ou valores.  
  
3.  Clique em **OK** para salvar as configurações.  
  
Você também pode personalizar as configurações para o projeto atual. As configurações são salvas no arquivo de projeto atual.  
  
**Para personalizar as configurações do projeto atual**  
  
1.  No menu **ferramentas** , clique em **ProjectSettings**.  
  
2.  Na caixa de diálogo **ProjectSettings** , use um dos seguintes procedimentos:  
  
    1.  Para selecionar um modo predefinido, selecione **padrão**, **otimista**ou **completo** na caixa suspensa **modo** .  
  
    2.  Para especificar um modo personalizado, selecione **personalizado** na caixa suspensa **modo** . E, em seguida, selecione as configurações de projeto apropriadas.  
  
3.  Clique em **OK** para salvar as configurações.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando MySQL e SQL Server tipos de dados &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Caso contrário, você pode converter as definições de objeto do banco de dados MySQL em SQL Server ou SQL Azure definições de objeto. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Mapeando tipos de dados MySQL e SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
