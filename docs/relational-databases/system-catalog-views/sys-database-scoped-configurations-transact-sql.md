---
title: sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da115c8d4cf48cfbcd6190c88a83bee4e61ae5a1
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240762"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys. database_scoped_configurations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Contém uma linha por configuração. 

|Nome da coluna|Tipo de Dados|Description|
|-----------------|---------------|-----------------|
|**configuration_id**|**Int**|ID da opção de configuração.|
|**name**|**nvarchar(60)**|O nome da opção de configuração. Para obter informações sobre as possíveis configurações, consulte [ALTER DATABASE Scoped &#40;Configuration Transact-&#41;SQL](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|**value**|**sqlvariant**|O valor definido para esta opção de configuração para a réplica primária.|
|**value_for_secondary**|**sqlvariant**|O valor definido para esta opção de configuração para as réplicas secundárias.|
|**is_value_default**|**bit** |Especifica se o valor definido é o valor padrão.|

## <a name="Permissions"></a> Permissões

Requer associação à função **pública** .

## <a name="remarks"></a>Remarks

Quando NULL é retornado como o valor de **value_for_secondary**, isso significa que o secundário está definido como PRIMARY.
 
As definições de configurações no escopo do banco de dados serão transferidas para o banco de dados. Isso significa que quando um determinado banco de dados é restaurado ou anexado, as definições de configuração existentes permanecem.

## <a name="see-also"></a>Consulte Também

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
