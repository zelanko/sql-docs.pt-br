---
title: Migrar bancos de dados MySQL para o SQL Server – BD SQL do Azure | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: badfb3afaeba92f366e62fce8dfcb3ec7dae9f29
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311957"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>Migrando bancos de dados MySQL para o SQL Server – BD SQL do Azure (MySQLToSql)
SQL Server SSMA (Migration Assistant) para MySQL é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados MySQL para o SQL Server ou SQL Azure. Usando o SSMA para MySQL, você pode examinar dados e objetos de banco de dados, avaliar os bancos de dados para a migração, migrar objetos de banco de dados para o SQL Server ou SQL Azure e, em seguida, migrar dados para o SQL Server ou SQL Azure.  
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito dados e objetos de bancos de dados MySQL para o SQL Server ou SQL Azure, use o seguinte processo:  
  
1.  [Trabalhando com projetos do SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, migração e conversão de projeto. Para obter mais informações sobre as configurações do projeto, consulte [definir opções do projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento MySQL e tipos de dados do SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [Conectar-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [Conectando ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [Mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Conectar-se ao banco de dados SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  Opcionalmente, [avaliando de bancos de dados MySQL para conversão de &#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
7.  [Converter bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [Sincronização](loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
9. Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo no SQL Server ou SQL Azure.  
  
    -   Sincronize os objetos de banco de dados.  
  
10. [Migrar dados do MySQL para o SQL Server – BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. Se necessário, atualize os aplicativos de banco de dados.  
  
> [!NOTE]  
> Você não pode migrar esquemas Information_schema e MySQL.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Introdução ao SSMA para MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
