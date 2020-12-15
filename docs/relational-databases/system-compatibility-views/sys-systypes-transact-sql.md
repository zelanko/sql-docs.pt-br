---
description: sys.systypes (Transact-SQL)
title: Tipos de sys.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bd2a68f151a136a5bb9de7efd170c7178d8001e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464667"
---
# <a name="syssystypes-transact-sql"></a>sys.systypes (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada tipo de dados definidos pelo usuário e fornecidos pelo sistema definidos no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do tipo de dados.|  
|**xtype**|**tinyint**|Tipo de armazenamento físico.|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|Tipo de usuário estendido. Estoura ou retorna NULL se o número de tipos de dados exceder 32.767.|  
|**length**|**smallint**|Comprimento físico do tipo de dados.|  
|**xprec**|**tinyint**|Precisão interna, como usado pelo servidor. Não deve ser usada em consultas.|  
|**xscale**|**tinyint**|Escala interna, como usada pelo servidor. Não deve ser usada em consultas.|  
|**tdefault**|**int**|ID do procedimento armazenado que contém verificações de integridade para este tipo de dados.|  
|**controlador**|**int**|ID do procedimento armazenado que contém verificações de integridade para este tipo de dados.|  
|**UID**|**smallint**|ID de esquema do proprietário do tipo.<br /><br /> Em bancos de dados atualizados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o ID de esquema é idêntico ao ID de usuário do proprietário.<br /><br /> Importante se você usar qualquer uma das seguintes instruções DDL, deverá usar a exibição de catálogo **\* Sys. Types em vez de tipossys.sys. \* \* \*** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) <br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**reservado**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**CollationID**|**int**|Se baseado em caractere, **CollationID** será a ID do agrupamento do banco de dados atual; caso contrário, será nulo.|  
|**UserType**|**smallint**|ID de tipo do usuário. Estoura ou retorna NULL se o número de tipos de dados exceder 32.767.|  
|**variable**|**bit**|Tipo de dados de comprimento variável.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**allownulls**|**bit**|Indica a nulabilidade padrão para este tipo de dados. Esse valor padrão é substituído por se a nulidade for especificada usando [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ou [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).|  
|**tipo**|**tinyint**|Tipo de dados de armazenamento físico.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|Nível de precisão para este tipo de dados.<br /><br /> -1 = **XML** ou tipos de valor grande.|  
|**scale**|**tinyint**|Escala para esse tipo de dados, com base na precisão.<br /><br /> NULL = Tipo de dados é não numérico.|  
|**Agrupamento**|**sysname**|Se baseado em caractere, o **agrupamento** será o agrupamento do banco de dados atual; caso contrário, será nulo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de compatibilidade &#40;&#41;Transact-SQL ](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
