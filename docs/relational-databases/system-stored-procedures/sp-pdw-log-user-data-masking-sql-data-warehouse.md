---
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-data-warehouse
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e401596add887d6bfc3f7fc7bd6b5255128b251c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_log_user_data_masking** para habilitar o mascaramento de dados do usuário [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade. O mascaramento de dados do usuário afeta as instruções em todos os bancos de dados no dispositivo.  
  
> [!IMPORTANT]  
>  O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade afetados por **sp_pdw_log_user_data_masking** são determinados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade. **sp_pdw_log_user_data_masking** não afeta os logs de transação do banco de dados, ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logs de erros.  
  
 **Plano de fundo:** na configuração padrão [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade completo contêm [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções e pode em alguns casos incluem dados de usuário contidos em operações como **inserir**, **Atualização**, e **selecione** instruções. No caso de um problema no dispositivo, isso permite que a análise das condições que causou o problema sem a necessidade de reproduzir o problema. Para impedir que os dados de usuário que está sendo gravada [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de atividades, os clientes podem optar por ativar o mascaramento de dados de usuário usando esse procedimento armazenado. As instruções ainda serão gravadas [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade, mas todos os literais em instruções que podem conter dados de usuário serão mascarados; substituído com alguns valores de constantes predefinidas.  
  
 Quando a criptografia transparente de dados está habilitada no dispositivo, o mascaramento de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de atividade é automaticamente ativado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parâmetros  
 [ **@masking_mode=** ] *masking_mode*  
 Determina se o mascaramento de dados de usuário transparente de dados criptografia log estão habilitados. *masking_mode* é **int**, e pode ser um dos seguintes valores:  
  
-   0 = desabilitado, o usuário dados aparecem no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade.  
  
-   1 = habilitado, o usuário instruções dados aparecem no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade, mas os dados do usuário é mascarado.  
  
-   2 = instruções que contém dados de usuário não são gravados para o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade.  
  
 Executar **sp_pdw_ log_user_data_masking** sem parâmetros reverte o estado atual do mascaramento de dados de usuário de log TDE no dispositivo como um conjunto de resultado escalar.  
  
## <a name="remarks"></a>Remarks  
 Mascaramento de dados do usuário [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] permite a substituição de literais de logs de atividades com valores constantes predefinidos em **selecione** e instruções DML, pois eles podem conter dados de usuário. Configuração *masking_mode* como 1 não mascara metadados, como nomes de coluna ou nomes de tabela. Configuração *masking_mode* 2 remove instruções com metadados, como nomes de coluna ou nomes de tabela.  
  
 Dados de usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de atividade é implementada da seguinte maneira:  
  
-   Dados TDE e do usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de atividade estão desativados por padrão. As instruções não serão automaticamente mascaradas se a criptografia de banco de dados não está habilitada no dispositivo.  
  
-   Habilitando a TDE no dispositivo automaticamente ativa o mascaramento de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de atividade.  
  
-   Desabilitando a TDE não afeta os dados de usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de atividade.  
  
-   Você pode habilitar explicitamente o mascaramento de dados do usuário [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade usando o **sp_pdw_log_user_data_masking** procedimento.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** função de banco de dados fixa ou **CONTROL SERVER** permissão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir permite que os dados de usuário de log TDE mascaramento no dispositivo.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_pdw_database_encryption &#40; SQL Data Warehouse &#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
