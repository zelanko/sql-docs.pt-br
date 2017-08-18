---
title: "Mapear relações muitos para muitos (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 393483c566c3e4b61833972ef2b33ba2dde8404a
ms.contentlocale: pt-br
ms.lasthandoff: 08/18/2017

---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>Mapear relações muitos para muitos (Visual Database Tools)
Relações muitos para muitos permitem relacionar cada linha em uma tabela a muitas linhas em outra tabela e vice-versa. Por exemplo, você pode criar uma relação muitos para muitos entre a tabela `authors` e a tabela `titles` para corresponder cada autor a todos os seus livros e corresponder cada livro a todos seus autores. Criar uma relação um para muitos de qualquer tabela indicaria incorretamente que cada livro pode ter somente um autor, ou que cada autor pode escrever somente um livro.  
  
Relações muitos para muitos entre tabelas são acomodadas em bancos de dados por meio de tabelas de junção. Uma tabela de junção contém as colunas de chave primária das duas tabelas que você deseja relacionar. Em seguida, você cria uma relação das colunas de chave primária de cada uma dessas duas tabelas para as colunas correspondentes na tabela de junção. No banco de dados pubs, a tabela `titleauthor` é a tabela de junção.  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>Para criar uma relação de muitos para muitos entre tabelas  
  
1.  No seu diagrama de banco de dados, adicione as tabelas que você deseja para criar uma relação muitos para muitos entre elas.  
  
2.  Crie uma terceira tabela clicando com o botão direito do mouse no diagrama e escolhendo **Nova Tabela** no menu de atalho. Essa se tornará a tabela de junção.  
  
3.  Na caixa de diálogo **Escolher Nome** , altere o nome da tabela atribuído pelo sistema. Por exemplo, a tabela de junção entre a tabela `titles` e a tabela `authors` é agora nomeada `titleauthors`.  
  
4.  Copie as colunas de chave primária de cada uma das duas outras tabelas para a tabela de junção. Você pode adicionar outras colunas a esta tabela, da mesma maneira que pode adicionar a qualquer outra tabela.  
  
5.  Na tabela de junção, defina a chave primária para incluir todas as colunas de chave primária das duas outras tabelas. Para obter detalhes, veja [Como criar chaves primárias (Visual Database Tools)](http://msdn.microsoft.com/en-us/85c623ca-4656-4d70-a9db-ee4d897cd214).  
  
6.  Defina uma relação um para muitos entre cada uma das duas tabelas primárias e a tabela de junção. A tabela de junção deve estar no lado "muitos" de ambas as relações que você criar. Para obter detalhes, veja [Como criar relações entre tabelas (Visual Database Tools)](http://msdn.microsoft.com/en-us/867a54b8-5be4-46e6-9702-49ae6dabf67c).  
  
    > [!NOTE]  
    > A criação de uma tabela de junção em um diagrama de banco de dados não insere dados das tabelas relacionadas na tabela de junção. Para obter informações sobre como inserir dados em uma tabela, veja [Criar consultas Inserir Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-insert-results-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte também  
[Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  

