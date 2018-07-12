---
title: Modificar um índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a34096c26200a2defbb8cac28f685fba9ac37fcc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37152367"
---
# <a name="modify-an-index"></a>Modificar um índice
  Este tópico descreve como modificar um índice no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Índices criados em decorrência de uma restrição PRIMARY KEY ou UNIQUE não podem ser modificados usando esse método. Em vez disso, a restrição deve ser modificada.  
  
 **Neste tópico**  
  
-   **Para modificar um índice, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-an-index"></a>Para modificar um índice  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda o **Banco de Dados**, expanda o banco de dados a que pertence a tabela e, depois, expanda **Tabelas**.  
  
3.  Expanda a tabela onde se encontra o índice e expanda **Índices**.  
  
4.  Clique com o botão direito do mouse no índice a ser modificado e selecione **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades de Índice** , faça as alterações desejadas. Por exemplo, você pode adicionar ou remover uma coluna da chave de índice, ou alterar a configuração de uma opção de índice.  
  
#### <a name="to-modify-index-columns"></a>Para modificar as colunas de um índice  
  
1.  Para adicionar, remover ou alterar a posição de uma coluna de um índice, selecione a página **Geral** na caixa de diálogo **Propriedades do Índice** .  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-an-index"></a>Para modificar um índice  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo descarta e recria um índice existente na coluna `ProductID` da tabela `Production.WorkOrder` usando a opção `DROP_EXISTING` . As opções `FILLFACTOR` e `PAD_INDEX` também são definidas.  
  
     [!code-sql[IndexDDL#CreateIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/createindex.sql#createindex4)]  
  
     O exemplo a seguir usa ALTER INDEX para definir várias opções no índice `AK_SalesOrderHeader_SalesOrderNumber`.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
#### <a name="to-modify-index-columns"></a>Para modificar as colunas de um índice  
  
1.  Para adicionar, remover ou alterar a posição de uma coluna de índice, você deve remover e recriar o índice.  
  
## <a name="see-also"></a>Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)   
 [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)   
 [sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)   
 [Opções Set Index](set-index-options.md)   
 [Renomear índices](indexes.md)  
  
  
