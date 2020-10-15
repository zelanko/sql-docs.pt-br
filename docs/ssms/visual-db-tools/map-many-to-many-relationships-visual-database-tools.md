---
description: Mapear relações muitos para muitos (Visual Database Tools)
title: Mapear relações de muitos para muitos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: afe40ef4863965905dedd825ee04bdb8a0e3e4d1
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038395"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>Mapear relações muitos para muitos (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Relações muitos para muitos permitem relacionar cada linha em uma tabela a muitas linhas em outra tabela e vice-versa. Por exemplo, você pode criar uma relação muitos para muitos entre a tabela `authors` e a tabela `titles` para corresponder cada autor a todos os seus livros e corresponder cada livro a todos seus autores. Criar uma relação um para muitos de qualquer tabela indicaria incorretamente que cada livro pode ter somente um autor, ou que cada autor pode escrever somente um livro.  
  
Relações muitos para muitos entre tabelas são acomodadas em bancos de dados por meio de tabelas de junção. Uma tabela de junção contém as colunas de chave primária das duas tabelas que você deseja relacionar. Em seguida, você cria uma relação das colunas de chave primária de cada uma dessas duas tabelas para as colunas correspondentes na tabela de junção. No banco de dados pubs, a tabela `titleauthor` é a tabela de junção.  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>Para criar uma relação de muitos para muitos entre tabelas  
  
1.  No seu diagrama de banco de dados, adicione as tabelas que você deseja para criar uma relação muitos para muitos entre elas.  
  
2.  Crie uma terceira tabela clicando com o botão direito do mouse no diagrama e escolhendo **Nova Tabela** no menu de atalho. Essa se tornará a tabela de junção.  
  
3.  Na caixa de diálogo **Escolher Nome** , altere o nome da tabela atribuído pelo sistema. Por exemplo, a tabela de junção entre a tabela `titles` e a tabela `authors` é agora nomeada `titleauthors`.  
  
4.  Copie as colunas de chave primária de cada uma das duas outras tabelas para a tabela de junção. Você pode adicionar outras colunas a esta tabela, da mesma maneira que pode adicionar a qualquer outra tabela.  
  
5.  Na tabela de junção, defina a chave primária para incluir todas as colunas de chave primária das duas outras tabelas. Para obter detalhes, veja o procedimento [Como criar chaves primárias](../../relational-databases/tables/create-primary-keys.md).  
  
6.  Defina uma relação um para muitos entre cada uma das duas tabelas primárias e a tabela de junção. A tabela de junção deve estar no lado "muitos" de ambas as relações que você criar. Para obter detalhes, veja o procedimento [Como criar relações entre tabelas](../../relational-databases/tables/create-foreign-key-relationships.md).  
  
    > [!NOTE]  
    > A criação de uma tabela de junção em um diagrama de banco de dados não insere dados das tabelas relacionadas na tabela de junção. Para obter informações sobre como inserir dados em uma tabela, veja [Criar consultas Inserir Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-insert-results-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
[Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
