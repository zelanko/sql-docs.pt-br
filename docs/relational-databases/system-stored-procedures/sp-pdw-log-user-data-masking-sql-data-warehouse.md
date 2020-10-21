---
description: sp_pdw_log_user_data_masking (Azure Synapse Analytics)
title: sp_pdw_log_user_data_masking (Azure Synapse Analytics) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c014f76aac1544e16ec693277a034779f75883cd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92255602"
---
# <a name="sp_pdw_log_user_data_masking-azure-synapse-analytics"></a>sp_pdw_log_user_data_masking (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Use **sp_pdw_log_user_data_masking** para habilitar o mascaramento de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade. A máscara de dados do usuário afeta as instruções em todos os bancos de dado no dispositivo.  
  
> [!IMPORTANT]  
>  Os [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade afetados por **sp_pdw_log_user_data_masking** são determinados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade. **sp_pdw_log_user_data_masking** não afeta os logs de transações do banco de dados ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os logs de erros.  
  
 **Plano de fundo:** Nos logs de atividade de configuração padrão [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] contêm [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções completas, e pode, em alguns casos, incluir dados de usuário contidos em operações, como instruções **Insert**, **Update**e **Select** . No caso de um problema no dispositivo, isso permite a análise das condições que causaram o problema sem a necessidade de reproduzir o problema. Para impedir que os dados do usuário sejam gravados nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividades, os clientes podem optar por ativar a máscara de dados do usuário usando esse procedimento armazenado. As instruções ainda serão gravadas nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividades, mas todos os literais em instruções que podem conter dados do usuário serão mascarados; substituídos por alguns valores constantes predefinidos.  
  
 Quando a Transparent Data Encryption está habilitada no dispositivo, o mascaramento dos dados do usuário nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade é automaticamente ativado.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### <a name="parameters"></a>Parâmetros  
`[ @masking_mode = ] masking_mode` Determina se a máscara de dados do usuário do log de criptografia de dados transparente está habilitada. *masking_mode* é **int**e pode ser um dos seguintes valores:  
  
-   0 = desabilitado, os dados do usuário aparecem nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade.  
  
-   1 = habilitado, as instruções de dados do usuário aparecem nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade, mas os dados do usuário são mascarados.  
  
-   2 = as instruções que contêm dados do usuário não são gravadas nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade.  
  
 A execução de **sp_pdw_ log_user_data_masking** sem parâmetros retorna o estado atual da máscara de dados do usuário do log TDE no dispositivo como um conjunto de resultados escalar.  
  
## <a name="remarks"></a>Comentários  
 A máscara de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividades permite a substituição de literais com valores constantes predefinidos em instruções **Select** e DML, pois eles podem conter dados do usuário. A definição de *masking_mode* como 1 não mascara metadados, como nomes de coluna ou nomes de tabela. Definir *masking_mode* como 2 remove instruções com metadados, como nomes de coluna ou nomes de tabela.  
  
 A máscara de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade é implementada da seguinte maneira:  
  
-   O TDE e a máscara de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade são desativados por padrão. As instruções não serão mascaradas automaticamente se a criptografia do banco de dados não estiver habilitada no dispositivo.  
  
-   A habilitação do TDE no dispositivo ativa automaticamente a máscara de dados do usuário nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade.  
  
-   Desabilitar o TDE não afeta a máscara de dados do usuário nos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade.  
  
-   Você pode habilitar explicitamente a máscara de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade usando o procedimento **sp_pdw_log_user_data_masking** .  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de banco de dados fixa **sysadmin** ou a permissão **Control Server** .  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita a máscara de dados do usuário de log do TDE no dispositivo.  
  
```sql  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_pdw_database_encryption &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
