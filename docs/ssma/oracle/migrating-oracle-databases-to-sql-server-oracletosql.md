---
title: Bancos de dados Oracle migrando para o SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
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
ms.openlocfilehash: c5137a8be3aa05b4d7f445e467750780ceba8c6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migrando bancos de dados Oracle para o SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA (Migration Assistant) para Oracle é um ambiente abrangente que ajuda a migrar rapidamente bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], banco de dados de SQL Azure ou Azure SQL Data Warehouse. Usando o SSMA para Oracle, você pode examinar os dados e objetos de banco de dados, avaliar bancos de dados para migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], banco de dados de SQL Azure ou Azure SQL Data Warehouse, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o banco de dados do Azure SQL ou de dados do SQL Azure Data warehouse. Observe que você não pode migrar esquemas SYS e sistema Oracle.
  
## <a name="recommended-migration-process"></a>Recomendado o processo de migração  
Para migrar com êxito os objetos e dados de bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], banco de dados de SQL Azure ou Azure SQL Data Warehouse, use o seguinte processo:
  
1.  [Criar um novo projeto SSMA](http://msdn.microsoft.com/en-us/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b).  
  
    Depois de criar o projeto, você pode definir opções de mapeamento de tipo, a migração e a conversão de projeto. Para obter informações sobre configurações de projeto, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeamento Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Conectar ao servidor de banco de dados Oracle](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
3.  [Conectar a uma instância do SQL Server](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
4.  [Mapear os esquemas de banco de dados Oracle para esquemas de banco de dados do SQL Server](http://msdn.microsoft.com/en-us/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc).  
  
5.  Opcionalmente, [criar relatórios de avaliação](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357) para avaliar os objetos de banco de dados para a conversão e estimar o tempo de conversão.  
  
6.  [Converter os esquemas de banco de dados Oracle em esquemas do SQL Server](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272).  
  
7.  [Carregar os objetos de banco de dados convertido no SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
    Você pode fazer isso em uma das seguintes maneiras:  
  
    -   Salvar um script e executá-lo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Sincronize os objetos de banco de dados.  
  
8.  [Migrar dados para o SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
9. Se necessário, atualize os aplicativos de banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Guia de Introdução com o SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
