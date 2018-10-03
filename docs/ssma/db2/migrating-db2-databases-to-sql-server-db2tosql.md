---
title: Bancos de dados do DB2 migrando para o SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5700ab7812498e4ff965d43405e8ea7b8f6f7e35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668554"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrando bancos de dados do DB2 para o SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA (Migration Assistant) for DB2 é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Usando o SSMA para DB2, você pode examinar os objetos de banco de dados e dados, avaliar os bancos de dados para a migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL DB, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure. Observe que você não pode migrar esquemas SYS e sistema DB2.  
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito a objetos e dados de bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou BD SQL do Azure, use o seguinte processo:  
  
1.  [Novo projeto SSMA](http://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, migração e conversão de projeto. Para obter informações sobre as configurações do projeto, consulte [configurações do projeto &#40;conversão&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) e seções relacionadas. Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento DB2 e tipos de dados do SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conectar-se ao banco de dados DB2](http://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Conectando ao SQL Server](http://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Mapear esquemas do DB2 para esquemas SQL Server](http://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Opcionalmente, [relatórios de avaliação](http://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter esquemas do DB2](http://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Carregar os objetos de banco de dados convertidos no SQL Server](http://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrando dados do DB2 para o SQL Server](http://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introdução ao SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
