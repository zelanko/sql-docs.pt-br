---
title: Migrando do Oracle bancos de dados para o SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 9e746d1df201349011d24fc0de007c74ba0073b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209800"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migração de bancos de dados Oracle para o SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA (Migration Assistant) para Oracle é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], BD SQL do Azure ou Azure SQL Data Warehouse. Usando o SSMA para Oracle, você pode examinar os objetos de banco de dados e dados, avaliar os bancos de dados para a migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], BD SQL do Azure ou SQL Data Warehouse do Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], BD SQL do Azure ou dados do SQL Azure Data warehouse. Observe que você não pode migrar esquemas SYS e sistema Oracle.
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito a objetos e dados de bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], BD SQL do Azure ou SQL Data Warehouse do Azure, use o seguinte processo:
  
1.  [Criar um novo projeto SSMA](working-with-ssma-projects-oracletosql.md).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, migração e conversão de projeto. Para obter informações sobre as configurações do projeto, consulte [definir opções do projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Conectar-se ao servidor de banco de dados Oracle](connecting-to-oracle-database-oracletosql.md).  
  
3.  [Conectar a uma instância do SQL Server](connecting-to-sql-server-oracletosql.md).  
  
4.  [Mapear esquemas de banco de dados Oracle para esquemas de banco de dados do SQL Server](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
5.  Opcionalmente, [crie relatórios de avaliação](assessing-oracle-schemas-for-conversion-oracletosql.md) avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter esquemas de banco de dados Oracle para esquemas SQL Server](converting-oracle-schemas-oracletosql.md).  
  
7.  [Carregar os objetos de banco de dados convertidos no SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
    Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrar dados para o SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Introdução ao SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
