---
title: Definir as opções de projeto (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5cbaeadbc97a178f3c90f43e26fc13cde416ecc5
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776642"
---
# <a name="setting-project-options-mysqltosql"></a>Definindo opções de projeto (MySQLToSQL)
Para cada projeto SSMA, você pode definir opções de nível de projeto. Essas opções especificam como os objetos são convertidos, como os dados são migrados e como os tipos de dados de origem são mapeados para tipos de dados de destino.  Antes de converter os objetos no SQL Server ou SQL Azure ou migrar dados para o SQL Server ou SQL Azure, verifique se as opções de configuração apropriadas para o projeto.  
  
O SSMA permite configurar as opções padrão para todos os projetos. Essas opções são aplicadas a qualquer novo projeto que você criar. Em seguida, você pode personalizar as opções para cada projeto.  
  
## <a name="configuration-options-and-modes"></a>Modos e opções de configuração  
O SSMA tem cinco conjuntos de configurações de projeto:  
  
-   Informações do projeto  
  
-   Geral (conversão, migração e do SQL Azure)  
  
-   Synchronization  
  
-   INTERFACE GRÁFICA DO USUÁRIO  
  
-   Mapeamento de tipo  
  
As configurações de projeto podem ser configuradas de quatro maneiras:  
  
-   Padrão  
  
-   Otimistas  
  
-   Completo  
  
-   Personalizar  
  
O padrão é recomendado para a maioria dos usuários. O modo otimista mantém mais da sintaxe do MySQL atual e é mais fácil de ler. No entanto, a manter a sintaxe atual pode não ser precisa. Se a sintaxe do MySQL deve ser convertida em sintaxe equivalente do SQL Server ou SQL Azure, o modo completo executa a conversão mais completa. No entanto, o código resultante, pode ser mais difícil de ler. No modo personalizado, você pode definir as opções.  
  
Para obter mais informações sobre as configurações e como as configurações são aplicadas em cada modo, consulte os tópicos a seguir:  
  
-   [Configurações do projeto &#40;conversão&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [Configurações do projeto &#40;migração&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [Configurações de projeto (GUI) (SSMA comum)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configurações do projeto &#40;mapeamento de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [Configurações do projeto &#40;sincronização&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [Configurações do projeto &#40;banco de dados SQL do Azure&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>Definindo opções de projeto  
Em SSMA, você pode configurar as configurações padrão para todos os projetos. Essas configurações são salvas no arquivo de configuração do SSMA e aplicadas a qualquer novo projeto que você criar.  
  
**Para definir opções de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, clique em **configurações de projeto padrão**.  
  
2.  No **configurações de projeto padrão** caixa de diálogo, use um dos procedimentos a seguir:  
  
    1.  Selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido e alterado de **versão de destino de migração** lista suspensa, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão ou migração ou SQL Azure** opção.  
  
    2.  Para selecionar um modo predefinido, selecione **padrão**, **Optimistic**, ou **completo** do **modo** caixa suspensa.  
  
    3.  Para especificar configurações personalizadas, selecione ou insira as configurações da nova ou valores.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
Você também pode personalizar as configurações para o projeto atual. As configurações salvo para o arquivo de projeto atual.  
  
**Para personalizar as configurações para o projeto atual**  
  
1.  Sobre o **ferramentas** menu, clique em **ProjectSettings**.  
  
2.  No **ProjectSettings** caixa de diálogo, use um dos procedimentos a seguir:  
  
    1.  Para selecionar um modo predefinido, selecione **padrão**, **Optimistic**, ou **completo** do **modo** caixa suspensa.  
  
    2.  Para especificar um modo personalizado, selecione **personalizado** do **modo** caixa suspensa. E, em seguida, selecione as configurações apropriadas do projeto.  
  
3.  Clique em **Okey** para salvar as configurações.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [tipos de dados do SQL Server e MySQL de mapeamento &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Caso contrário, você pode converter as definições de objeto de banco de dados MySQL no SQL Server ou definições de objeto do SQL Azure. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Mapeamento de tipos de dados do SQL Server e MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
