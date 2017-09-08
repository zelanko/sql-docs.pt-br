---
title: Migrar bancos de dados MySQL para o SQL Server - banco de dados SQL do Azure | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d86a7d779212a781a4bab29a85a963cf163b9ade
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>Migrando bancos de dados MySQL para o SQL Server - banco de dados do SQL Azure (MySQLToSql)
SQL Server SSMA (Migration Assistant) para MySQL é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados MySQL para o SQL Server ou SQL Azure. Usando o SSMA para MySQL, você pode examinar os dados e objetos de banco de dados, avaliar bancos de dados para migração, migrar objetos de banco de dados do SQL Server ou SQL Azure e, em seguida, migrar dados para o SQL Server ou SQL Azure.  
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito objetos e dados de bancos de dados MySQL para o SQL Server ou SQL Azure, use o seguinte processo:  
  
1.  [Trabalhando com projetos do SSMA &#40; MySQLToSQL &#41; ](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, a migração e a conversão de projeto. Para obter mais informações sobre configurações de projeto, consulte [definindo opções de projeto &#40; MySQLToSQL &#41; ](../../ssma/mysql/setting-project-options-mysqltosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento MySQL e tipos de dados do SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [Conectando ao MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [Conectar-se ao SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [Mapeamento de bancos de dados MySQL para esquemas SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Conectar-se ao banco de dados SQL do Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  Opcionalmente, [avaliando os bancos de dados MySQL para conversão &#40; MySQLToSQL &#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) para avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
7.  [Conversão de bancos de dados MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [Sincronização](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
9. Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo no SQL Server ou SQL Azure.  
  
    -   Sincronize os objetos de banco de dados.  
  
10. [Migração de dados MySQL para o SQL Server - banco de dados SQL do Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. Se necessário, atualize os aplicativos de banco de dados.  
  
> [!NOTE]  
> Você não pode migrar esquemas Information_schema e MySQL.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para MySQL &#40; MySqlToSql &#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Guia de Introdução com o SSMA para MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  

