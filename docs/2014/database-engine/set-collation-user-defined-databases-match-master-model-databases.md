---
title: Definir o agrupamento de bancos de dados definidos pelo usuário para corresponder aos dos bancos de dados mestre e modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b48696fb56c40062d62f04845715170887f84fda
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929147"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>Definir a ordenação de bancos de dados definidos pelo usuário para corresponder aos dos bancos de dados mestre e modelo
  Esta regra verifica se os bancos de dados definidos pelo usuário são definidos usando uma ordenação de banco de dados com a mesma ordenação para mestre ou modelo.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que as ordenações de bancos de dados definidos pelo usuário correspondam à ordenação de mestre ou modelo. Caso contrário, conflitos de ordenação podem ocorrer, o que pode impedir a execução do código. Por exemplo, quando um procedimento armazenado une uma tabela a uma tabela temporária, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode finalizar o lote e retornar um erro de conflito de ordenação, se as ordenações do banco de dados definido pelo usuário e do banco de dados modelo forem diferentes. Isto ocorre porque tabelas temporárias são criadas em tempdb, o que serve como base para a ordenação daquele modelo.  
  
 Se surgirem erros de conflito de ordenação, considere uma das seguintes soluções:  
  
-   Exporte os dados do banco de dados do usuário e importe-os em novas tabelas com a mesma ordenação que os bancos de dados mestre e modelo.  
  
-   Recrie os bancos de dados do sistema para usar uma ordenação que corresponda à ordenação do banco de dados do usuário. Para obter mais informações sobre como recriar os bancos de dados do sistema, consulte [Recompilar bancos de dados do sistema](../relational-databases/databases/system-databases.md).  
  
-   Modifique os procedimentos armazenados que uniram as tabelas do usuário às tabelas em tempdb para criar tabelas no tempdb usando a ordenação do banco de dados do usuário. Para isso, adicione a cláusula `COLLATE database_default` às definições de coluna da tabela temporária, como demonstrado no exemplo a seguir:  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Definir ou alterar a ordenação de banco de dados](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [Definir ou alterar a ordenação de coluna](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Artigo 325335 da base de dados de conhecimento Microsoft](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [Como instalar o SQL Server 2008 pelo prompt de comando](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
