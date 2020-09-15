---
title: Definir a ordenação de bancos de dados definidos pelo usuário para corresponder aos dos bancos de dados mestre e modelo
description: Saiba como habilitar uma política para verificar se as ordenações de bancos de dados definidos pelo usuário e de bancos de dados do sistema são as mesmas.
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 905accc62afdc12152110d44a18e61d4c8a9bcef
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284836"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-master-and-model-databases"></a>Definir a ordenação de bancos de dados definidos pelo usuário para corresponder aos dos bancos de dados mestre e modelo
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica se os bancos de dados definidos pelo usuário são definidos usando uma ordenação de banco de dados com a mesma ordenação para mestre ou modelo.
  
## <a name="best-practices-recommendations"></a>Recomendações de melhores práticas  
 Recomendamos que as ordenações de bancos de dados definidos pelo usuário correspondam à ordenação de mestre ou modelo. Caso contrário, conflitos de ordenação podem ocorrer, o que pode impedir a execução do código. Por exemplo, quando um procedimento armazenado une uma tabela a uma tabela temporária, o SQL Server pode finalizar o lote e retornar um erro de conflito de ordenação se as ordenações do banco de dados definido pelo usuário e modelo de banco de dados são diferentes. Isto ocorre porque tabelas temporárias são criadas em tempdb, o que serve como base para a ordenação daquele modelo.

  Se surgirem erros de conflito de ordenação, considere uma das seguintes soluções:

  - Exporte os dados do banco de dados do usuário e importe-os em novas tabelas com a mesma ordenação que os bancos de dados mestre e modelo.

  - Recrie os bancos de dados do sistema para usar uma ordenação que corresponda à ordenação do banco de dados do usuário. Para obter mais informações sobre como recompilar os bancos de dados do sistema, confira [Recompilar bancos de dados do sistema](../databases/rebuild-system-databases.md).

  - Modifique os procedimentos armazenados que uniram as tabelas do usuário às tabelas em tempdb para criar tabelas no tempdb usando a ordenação do banco de dados do usuário. Para fazer isso, adicione a cláusula COLLATE database_default às definições de coluna da tabela temporária, conforme mostrado no seguinte exemplo:
  
    ```
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )
    ```

## <a name="see-also"></a>Veja também
  
 [Definir ou alterar a ordenação do servidor](../collations/set-or-change-the-server-collation.md)  

 [Definir ou alterar a ordenação de banco de dados](../collations/set-or-change-the-database-collation.md)

 [Definir ou alterar a ordenação de coluna](../collations/set-or-change-the-column-collation.md)
 
 [Exibir informações de ordenação](../collations/view-collation-information.md)    
  
  
