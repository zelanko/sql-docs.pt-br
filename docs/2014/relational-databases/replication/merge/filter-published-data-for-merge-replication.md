---
title: Filtrar dados publicados para replicação de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], filtering published data
- replication [SQL Server], filtering published data
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5558a5f3deaa0cfe7f44e8dfbbe96d5b8301442a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009114"
---
# <a name="filter-published-data-for-merge-replication"></a>Filtrar dados publicados para replicação de mesclagem
  Além dos filtros de linhas estáticas e filtros de colunas que você pode definir com outros tipos de replicação, a replicação de mesclagem oferece filtros de linhas com parâmetros e filtros de junção Para mais informações sobre filtros de linha estáticos e filtros de coluna, consulte [Filtrar dados publicados](../publish/filter-published-data.md).  
  
 A replicação de mesclagem é usada em muitos aplicativos para oferecer suporte a usuários móveis, esses aplicativos costumam ter um grande número de assinaturas com cada assinatura, recebendo um conjunto de dados exclusivo. Filtros com parâmetros, combinados com filtros de junção, permitem que um administrador defina uma publicação (ou no máximo um pequeno número de publicações) e forneça diferentes conjuntos de dados para usuários, reduzindo o gerenciamento de sobrecarga introduzido pela criação de múltiplas publicações.  
  
-   Os filtros com parâmetros permitem que diferentes partições de dados sejam enviados à diferentes Assinaturas sem a necessidade de que sejam criadas múltiplas publicações. Por exemplo, uma tabela pode ser filtrada para que os dados de um determinado representante de vendas seja replicado apenas para aquele representante. Os filtros com parâmetros têm uma variedade de opções que permitem o ajuste da filtragem para otimizar o desempenho e melhor correspondência aos dados e requisitos do aplicativo. Para saber mais, confira [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md).  
  
-   Os filtros de junção são usados normalmente em conjunto com filtros com parâmetros para estender a filtragem às tabelas relacionadas (também podem ser usados em conjunto com os filtros estáticos). Por exemplo, o representante de vendas geralmente tem dados em outras tabelas como as tabelas de clientes e pedidos. Esses dados podem ser filtrados para que o representante de vendas recebe apenas os dados sobre seus clientes e pedidos de seus clientes. Para obter mais informações, consulte [Join Filters](join-filters.md).  
  
 Um filtro não deve incluir o `rowguidcol` usado por replicação para identificar linhas. Por padrão, esta é a coluna adicionada no momento que você define a replicação de mesclagem e é denominada **rowguid**.  
  
## <a name="see-also"></a>Consulte também  
 [Publicar dados e objetos de banco de dados](../publish/publish-data-and-database-objects.md)  
  
  