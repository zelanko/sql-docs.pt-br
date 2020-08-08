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
ms.openlocfilehash: c0a762cbe49a3186a29feb5aa3424b083d2f8978
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933737"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrando bancos de dados DB2 para SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para DB2 é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados DB2 para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database. Usando o SSMA para DB2, você pode examinar os objetos e os dados do banco de dados, avaliar os bancos de dado para migração, migrar objetos de banco de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL Database e, em seguida, migrar dados para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL. Observe que não é possível migrar os esquemas SYS e SYSTEM DB2.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e os dados de bancos de dados DB2 para o ou o banco de dado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL do Azure, use o seguinte processo:  
  
1.  [Novo projeto do SSMA](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Depois de criar o projeto, você pode definir opções de conversão de projeto, migração e mapeamento de tipo. Para obter informações sobre configurações de projeto, consulte [configurações de projeto &#40;conversão&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) e seções relacionadas. Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mappinging DB2 and SQL Server Data Types &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conecte-se ao banco de dados DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Conectando-se a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Mapeie esquemas do DB2 para esquemas de SQL Server](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Opcionalmente, os [relatórios de avaliação](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) para avaliar objetos de banco de dados para conversão e estimar o tempo de conversão.  
  
6.  [Converta os esquemas do DB2](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Carregue os objetos de banco de dados convertidos em SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Você pode fazer isso de uma das seguintes maneiras:  
  
    -   Salve um script e execute-o no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrar dados do DB2 para o SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Instalando o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introdução com o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
