---
title: Habilitar e desabilitar o controle de alterações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], disabling
- data changes [SQL Server]
- change tracking [SQL Server], enabling
- tracking data changes [SQL Server]
- change tracking [SQL Server], configuring
- data [SQL Server], changing
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
author: rothja
ms.author: jroth
ms.openlocfilehash: 402c63ae03df14e3a725fbc440575f5233d502f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037331"
---
# <a name="enable-and-disable-change-tracking-sql-server"></a>Habilitar e desabilitar o controle de alterações (SQL Server)
  Este tópico descreve como habilitar e desabilitar o controle de alterações para um banco de dados e uma tabela.  
  
## <a name="enable-change-tracking-for-a-database"></a>Habilitar o controle de alterações para um banco de dados  
 Antes de usar o controle de alterações, você deve habilitar o controle de alterações no nível de banco de dados. O exemplo a seguir mostra como habilitar o controle de alterações usando [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 Você também pode habilitar o controle de alterações no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando a caixa de diálogo [Propriedades do Banco de Dados &#40;Página Controle de Alterações&#41;](../databases/database-properties-changetracking-page.md) .  
  
 Você pode especificar as opções CHANGE_RETENTION e AUTO_CLEANUP quando habilitar o controle de alterações e alterar os valores a qualquer momento depois que o controle de alterações estiver habilitado.  
  
 O valor de retenção determina o período de tempo que o controle de alterações mantém as informações. Informações do controle de alterações anteriores a esse período de tempo são removidas periodicamente. Quando estiver definindo esse valor, deverá considerar com que frequência os aplicativos serão sincronizados com as tabelas no banco de dados. O período de retenção especificado deve ter pelo menos a duração do período de tempo máximo entre as sincronizações. Se um aplicativo obtém as alterações em intervalos maiores, os resultados retornados podem ser incorretos porque algumas informações de alterações podem ter sido removidas. Para evitar resultados incorretos, um aplicativo pode usar a função de sistema CHANGE_TRACKING_MIN_VALID_VERSION para determinar se o intervalo entre as sincronizações foi muito longo.  
  
 Use a opção AUTO_CLEANUP para habilitar ou desabilitar a tarefa de limpeza que remove informações antigas de controle de alterações. Isso pode ser útil quando há um problema temporário que impede os aplicativos de sincronizarem e o processo para remover as informações do controle de alterações anterior ao período de retenção precisa ser interrompido até que o problema seja resolvido.  
  
 Para qualquer banco de dados que use o controle de alterações, lembre-se do seguinte:  
  
-   Para usar o controle de alterações, o nível de compatibilidade do banco de dados deve ser definido como 90 ou mais. Se o nível de compatibilidade de um banco de dados for inferior a 90, você poderá configurar o controle de alterações. No entanto, a função CHANGETABLE, usada para obter informações do controle de alterações, retornará um erro.  
  
-   Usar o isolamento do instantâneo é o modo mais fácil de garantir que todas as informações do controle de alterações sejam consistentes. Por esse motivo, é estritamente recomendável que o isolamento do instantâneo seja definido como ON para o banco de dados. Para obter mais informações, veja [Trabalhar com o controle de alterações &#40;SQL Server&#41;](work-with-change-tracking-sql-server.md).  
  
## <a name="enable-change-tracking-for-a-table"></a>Habilitar o controle de alterações para uma tabela  
 O controle de alterações deve ser habilitado para cada tabela que você deseja controlar. Quando o controle de alterações está habilitado, são mantidas informações sobre todas as linhas da tabela afetadas por uma operação DML.  
  
 O exemplo a seguir mostra como habilitar o controle de alterações para uma tabela usando [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
```sql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 Você também pode habilitar o controle de alterações para uma tabela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando a caixa de diálogo [Propriedades do Banco de Dados &#40;Página Controle de Alterações&#41;](../databases/database-properties-changetracking-page.md) .  
  
 Quando a opção TRACK_COLUMNS_UPDATED é definida como ON, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] armazena informações extras sobre quais colunas foram atualizadas na tabela interna de controle de alterações. O controle de coluna pode permitir a um aplicativo sincronizar apenas as colunas que foram atualizadas. Isso pode melhorar a eficiência e o desempenho. Entretanto, como a manutenção de informações do controle de alterações aumenta a sobrecarga de armazenamento, essa opção é definida como OFF por padrão.  
  
## <a name="disable-change-tracking-for-a-database-or-table"></a>Desabilitar o controle de alterações para um banco de dados ou uma tabela  
 É necessário desabilitar o controle de alterações em todas as tabelas com alterações controladas, antes que o controle de alterações seja definido como OFF no banco de dados. Para determinar as tabelas que tenham o controle de alterações habilitadas em um banco de dados, use a exibição do catálogo [sys.change_tracking_tables](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables) .  
  
 Quando nenhuma tabela de um banco de dados controlar as alterações, você pode desabilitar o controle de alterações no banco de dados. O exemplo a seguir mostra como desabilitar o controle de alterações para um banco de dados usando [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 O exemplo a seguir mostra como desabilitar o controle de alterações para uma tabela usando [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
```sql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do Banco de Dados &#40;Página Controle de Alterações&#41;](../databases/database-properties-changetracking-page.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)   
 [Controle de alterações de dados &#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [Sobre o controle de alterações &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md)   
 [Trabalhar com dados de alterações &#40;SQL Server&#41;](work-with-change-data-sql-server.md)   
 [Gerenciar o controle de alterações &#40;SQL Server&#41;](manage-change-tracking-sql-server.md)  
  
  
