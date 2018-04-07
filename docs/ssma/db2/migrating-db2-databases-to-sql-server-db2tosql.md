---
title: Bancos de dados DB2 migrando para o SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c908cafeb92acc982bb74d96c4cc6fc2f40bf9a6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrando bancos de dados do DB2 para o SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA (Migration Assistant) for DB2 é um ambiente abrangente que ajuda a migrar rapidamente bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Usando o SSMA para DB2, você pode examinar os dados e objetos de banco de dados, avaliar bancos de dados para migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Observe que você não pode migrar esquemas SYS e sistema DB2.  
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito os objetos e dados de bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do Azure SQL DB, use o seguinte processo:  
  
1.  [Novo projeto SSMA](http://msdn.microsoft.com/en-us/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, a migração e a conversão de projeto. Para obter informações sobre configurações de projeto, consulte [configurações de projeto &#40;conversão&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) e seções relacionadas. Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento DB2 e tipos de dados do SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conecte-se ao banco de dados DB2](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Conectando ao SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Mapear os esquemas de DB2 para esquemas SQL Server](http://msdn.microsoft.com/en-us/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Opcionalmente, [relatórios de avaliação](http://msdn.microsoft.com/en-us/9e13eba0-e3cf-4205-974f-c00f982061de) para avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter esquemas DB2](http://msdn.microsoft.com/en-us/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Carregar os objetos de banco de dados convertido no SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrando dados do DB2 no SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Guia de Introdução com o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
