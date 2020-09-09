---
description: sys.configurations (Transact-SQL)
title: sys.configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.configurations_TSQL
- configurations
- sys.configurations
- configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.configurations catalog view
ms.assetid: c4709ed1-bf88-4458-9e98-8e9b78150441
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6273f057b7733b787ed2ed8e8b61d23fd107fbd7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546816"
---
# <a name="sysconfigurations-transact-sql"></a>sys.configurations (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada valor de opção de configuração em todo o servidor no sistema.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Identificação exclusivo do valor de configuração.|  
|**name**|**nvarchar(35)**|O nome da opção de configuração.|  
|**value**|**sql_variant**|Valor configurado dessa opção.|  
|**minimum**|**sql_variant**|Valor mínimo para a opção de configuração.|  
|**maximum**|**sql_variant**|Valor máximo para a opção de configuração.|  
|**value_in_use**|**sql_variant**|Valor de execução atualmente em efeito dessa opção.|  
|**descrição**|**nvarchar(255)**|Descrição da opção de configuração.|  
|**is_dynamic**|**bit**|1 = A variável é implementada quando a instrução RECONFIGURE é executada.|  
|**is_advanced**|**bit**|1 = a variável é exibida somente quando a **exibição advancedoption** é definida.|  
  
 ## <a name="remarks"></a>Comentários
  Para obter uma lista de todas as opções de configuração do servidor, consulte [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!NOTE]  
>  Para obter opções de configuração no nível do banco de dados, consulte [ALTER DATABASE scopeed configuration &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar o soft-NUMA, consulte [Soft-numa &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
 
A exibição de catálogo sys.configurations pode ser usada para determinar a config_value (a coluna de valor), a run_value (a coluna de value_in_use) e se a opção de configuração é dinâmica (não requer uma reinicialização do mecanismo do servidor ou a coluna is_dynamic).

> [!NOTE]
> O config_value no conjunto de resultados de sp_configure é equivalente à coluna **sys.configurations. Value** . O **run_value** é equivalente à coluna **sys.configurations. value_in_use** .

A consulta a seguir pode ser usada para determinar se os valores configurados não foram instalados:

```SQL
select * from sys.configurations where value != value_in_use
```

Se o valor for igual à alteração da opção de configuração que você fez, mas o **value_in_use** não for o mesmo, o comando RECONFIGURE não será executado ou terá falhado ou o mecanismo do servidor deverá ser reiniciado.

Há opções de configuração nas quais o valor e a value_in_use podem não ser iguais e esse é um comportamento esperado. Por exemplo:

"Max Server Memory (MB)"-o valor padrão configurado de 0 será exibido como value_in_use = 2147483647 "min Server Memory (MB)"-o valor padrão configurado de 0 pode aparecer como value_in_use = 8 (32 bits) ou 16 (64 bits). 

Em alguns casos, o **value_in_use** será 0. Nessa situação, o **value_in_use** "verdadeiro" é 8 (32 bits) ou 16 (64 bits)

A coluna **is_dynamic** pode ser usada para determinar se a opção de configuração requer uma reinicialização. is_dynamic = 1 significa que quando o comando reconfigure (T-SQL) for executado, o novo valor entrará em vigor "imediatamente" (em alguns casos, o mecanismo do servidor poderá não avaliar o novo valor imediatamente, mas fará isso no curso normal de sua execução). is_dynamic = 0 significa que o valor de configuração alterado não entrará em vigor até que o servidor seja reiniciado, mesmo que o comando reconfigure (T-SQL) tenha sido executado.

Para uma opção de configuração que não é dinâmica, não há como saber se o comando reconfigure (T-SQL) foi executado para executar a primeira etapa de instalação da alteração de configuração. Antes de reiniciar SQL Server para instalar uma alteração de configuração, execute o comando reconfigure (T-SQL) para garantir que todas as alterações de configuração terão efeito após uma reinicialização SQL Server. 
 
 
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do catálogo de configuração em todo o servidor &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
