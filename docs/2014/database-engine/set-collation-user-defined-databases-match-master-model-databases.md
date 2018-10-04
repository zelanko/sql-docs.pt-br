---
title: Defina os bancos de dados definido pelo agrupamento de usuário para corresponder do mestre e bancos de dados modelo | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6aea5507c008d608b7fcc9e50c7defcdff90924d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190396"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>Definir o agrupamento de bancos de dados definidos pelo usuário para corresponder aos dos bancos de dados mestre e modelo
  Esta regra verifica se os bancos de dados definidos pelo usuário são definidos usando um agrupamento de banco de dados com o mesmo agrupamento para mestre ou modelo.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que os agrupamentos de bancos de dados definidos pelo usuário correspondam ao agrupamento de mestre ou modelo. Caso contrário, conflitos de agrupamento podem ocorrer, o que pode impedir a execução do código. Por exemplo, quando um procedimento armazenado une uma tabela a uma tabela temporária, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode finalizar o lote e retornar um erro de conflito de agrupamento, se os agrupamentos do banco de dados definido pelo usuário e do banco de dados modelo forem diferentes. Isto ocorre porque tabelas temporárias são criadas em tempdb, o que serve como base para o agrupamento daquele modelo.  
  
 Se surgirem erros de conflito de agrupamento, considere um das seguintes soluções:  
  
-   Exporte os dados do banco de dados do usuário e importe-os em novas tabelas com o mesmo agrupamento que os bancos de dados mestre e modelo.  
  
-   Recrie os bancos de dados do sistema para usar um agrupamento que corresponda ao agrupamento do banco de dados do usuário. Para obter mais informações sobre como recriar os bancos de dados do sistema, consulte [recriar bancos de dados do sistema](../relational-databases/databases/system-databases.md).  
  
-   Modifique os procedimentos armazenados que uniram as tabelas do usuário às tabelas em tempdb para criar tabelas no tempdb usando o agrupamento do banco de dados do usuário. Para isso, adicione a cláusula `COLLATE database_default` às definições de coluna da tabela temporária, como demonstrado no exemplo a seguir:  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Definir ou alterar o agrupamento de banco de dados](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [Definir ou alterar o agrupamento de coluna](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Artigo da Base de Conhecimento Microsoft 325335](http://go.microsoft.com/fwlink/?linkid=117751)  
  
 [Como: instalar o SQL Server 2008 do Prompt de comando](http://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
