---
title: Migrando do Oracle bancos de dados para o SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: f20b7271932cbbcc0538fc9923e45b2fc029f646
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983198"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migrando bancos de dados Oracle para o SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA (Migration Assistant) para Oracle é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], BD SQL do Azure ou Azure SQL Data Warehouse. Usando o SSMA para Oracle, você pode examinar os objetos de banco de dados e dados, avaliar os bancos de dados para a migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], BD SQL do Azure ou SQL Data Warehouse do Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], BD SQL do Azure ou dados do SQL Azure Data warehouse. Observe que você não pode migrar esquemas SYS e sistema Oracle.
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito a objetos e dados de bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], BD SQL do Azure ou SQL Data Warehouse do Azure, use o seguinte processo:
  
1.  [Criar um novo projeto SSMA](http://msdn.microsoft.com/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, migração e conversão de projeto. Para obter informações sobre as configurações do projeto, consulte [definir opções do projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Conectar-se ao servidor de banco de dados Oracle](http://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
3.  [Conectar a uma instância do SQL Server](http://msdn.microsoft.com/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
4.  [Mapear esquemas de banco de dados Oracle para esquemas de banco de dados do SQL Server](http://msdn.microsoft.com/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc).  
  
5.  Opcionalmente, [crie relatórios de avaliação](http://msdn.microsoft.com/4de9bcf6-1346-4740-87f9-7f24a8226357) avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter esquemas de banco de dados Oracle para esquemas SQL Server](http://msdn.microsoft.com/e021182d-31da-443d-b110-937f5db27272).  
  
7.  [Carregar os objetos de banco de dados convertidos no SQL Server](http://msdn.microsoft.com/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
    Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrar dados para o SQL Server](http://msdn.microsoft.com/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Introdução ao SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
