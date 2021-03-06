---
title: Migrando bancos de dados DB2 para SQL Server (DB2ToSQL) | Microsoft Docs
description: Use esse processo recomendado para migrar bancos de dados DB2 para o SQL Server ou o Azure SQL Database usando o Assistente de Migração do SQL Server (SSMA).
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e31d4b1d31cb186276d8424f8c49450cb4ce9406
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869524"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrando bancos de dados DB2 para SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Assistente de Migração (SSMA) para DB2 é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados DB2 para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database. Usando o SSMA para DB2, você pode examinar os objetos e os dados do banco de dados, avaliar os bancos de dado para migração, migrar objetos de banco de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL Database e, em seguida, migrar dados para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL. Observe que não é possível migrar os esquemas SYS e SYSTEM DB2.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e os dados de bancos de dados DB2 para o ou o banco de dado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL do Azure, use o seguinte processo:  
  
1.  [Novo projeto do SSMA](./new-project-db2tosql.md).  
  
    Depois de criar o projeto, você pode definir opções de conversão de projeto, migração e mapeamento de tipo. Para obter informações sobre configurações de projeto, consulte [configurações de projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) e seções relacionadas. Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mappinging DB2 and SQL Server Data Types &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conecte-se ao banco de dados DB2](./connecting-to-db2-database-db2tosql.md).  
  
3.  [Conectando-se a SQL Server](./connecting-to-sql-server-db2tosql.md).  
  
4.  [Mapeie esquemas do DB2 para esquemas de SQL Server](./mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
5.  Opcionalmente, os [relatórios de avaliação](./assessment-report-db2tosql.md) para avaliar objetos de banco de dados para conversão e estimar o tempo de conversão.  
  
6.  [Converta os esquemas do DB2](./converting-db2-schemas-db2tosql.md).  
  
7.  [Carregue os objetos de banco de dados convertidos em SQL Server](./loading-converted-database-objects-into-sql-server-db2tosql.md).  
  
    Você pode fazer isso de uma das seguintes maneiras:  
  
    -   Salve um script e execute-o no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrar dados do DB2 para o SQL Server](./migrating-db2-data-into-sql-server-db2tosql.md).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Instalando o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introdução com o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
