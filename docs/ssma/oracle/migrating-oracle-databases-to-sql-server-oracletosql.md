---
title: Migrando bancos de dados Oracle para SQL Server (OracleToSQL) | Microsoft Docs
description: Use esse processo recomendado para migrar bancos de dados Oracle para SQL Server ou para o Azure SQL Database usando o Assistente de Migração do SQL Server (SSMA).
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 67fb6eeba0a1385d3d764dfa2d8e55f40f34455a
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84294043"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migração de bancos de dados Oracle para o SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para Oracle é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados Oracle para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o BD SQL do Azure ou o azure SQL data warehouse. Usando o SSMA para Oracle, você pode examinar os objetos e os dados do banco de dados, avaliar os bancos de dado para migração, migrar objetos de banco de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o BD SQL do Azure ou o azure SQL data warehouse e, em seguida, migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o BD SQL do Azure ou o Azure SQL data warehouse. Observe que você não pode migrar esquemas SYS e do sistema Oracle.
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito objetos e dados de bancos de dados Oracle para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o BD SQL do Azure ou o azure SQL data warehouse, use o seguinte processo:
  
1.  [Crie um novo projeto do SSMA](working-with-ssma-projects-oracletosql.md).  
  
    Depois de criar o projeto, você pode definir opções de conversão de projeto, migração e mapeamento de tipo. Para obter informações sobre configurações de projeto, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeando os tipos de dados Oracle e SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Conecte-se ao servidor de banco de dados Oracle](connecting-to-oracle-database-oracletosql.md).  
  
3.  [Conecte-se a uma instância do SQL Server](connecting-to-sql-server-oracletosql.md).  
  
4.  [Mapeie esquemas de banco de dados Oracle para SQL Server esquemas de banco de dados](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
5.  Opcionalmente, [Crie relatórios de avaliação](assessing-oracle-schemas-for-conversion-oracletosql.md) para avaliar objetos de banco de dados para conversão e estimar o tempo de conversão.  
  
6.  [Converta esquemas de banco de dados Oracle em esquemas de SQL Server](converting-oracle-schemas-oracletosql.md).  
  
7.  [Carregue os objetos de banco de dados convertidos em SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
    Você pode fazer isso de uma das seguintes maneiras:  
  
    -   Salve um script e execute-o no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migre dados para SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Instalação do SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Introdução com o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
