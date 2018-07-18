---
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 16de9489583cce2e696a94c75c7e5fd3ac1c0fe1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993708"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_log_user_data_masking** para habilitar dados de usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade. Mascaramento de dados do usuário afeta as instruções em todos os bancos de dados no dispositivo.  
  
> [!IMPORTANT]  
>  O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade é afetado pela **sp_pdw_log_user_data_masking** são determinadas [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade. **sp_pdw_log_user_data_masking** não afeta os logs de transação do banco de dados, ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logs de erros.  
  
 **Em segundo plano:** na configuração padrão [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade completo contenham [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções e pode em alguns casos incluem dados de usuário contidos em operações como **inserir**,  **ATUALIZAÇÃO**, e **selecione** instruções. Caso haja um problema no dispositivo, isso permite que a análise das condições que causou o problema sem a necessidade de reproduzir o problema. Para impedir que os dados de usuário que estão sendo gravados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividades, os clientes podem escolher ativar o mascaramento de dados do usuário usando esse procedimento armazenado. As instruções ainda serão gravadas [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade, mas todos os literais de instruções que podem conter dados de usuário serão mascarados; substituído com alguns valores de constantes predefinidas.  
  
 Quando a criptografia transparente de dados está habilitada no dispositivo, de mascaramento dos dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividades é ativado automaticamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parâmetros  
 [  **@masking_mode=** ] *masking_mode*  
 Determina se a transparent data encryption log usuário mascaramento de dados estão habilitados. *masking_mode* está **int**, e pode ser um dos seguintes valores:  
  
-   0 = desabilitada, o usuário dados aparecem no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade.  
  
-   1 = Enabled, o usuário as instruções de dados aparecem no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade, mas os dados do usuário sejam mascarados.  
  
-   2 = instruções contendo dados de usuário não são gravados a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade.  
  
 Executando **sp_pdw_ log_user_data_masking** sem parâmetros reverte o estado atual da máscara de dados de usuário de log TDE no dispositivo como um conjunto de resultado escalar.  
  
## <a name="remarks"></a>Remarks  
 Dados de usuário de mascaramento na [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] permite a substituição de literais de logs de atividades com valores constantes predefinidas na **selecione** e instruções DML, como eles podem conter dados de usuário. Definindo *masking_mode* como 1 não mascara metadados, como nomes de coluna ou tabela. Definindo *masking_mode* 2 remove as instruções com metadados, como nomes de coluna ou tabela.  
  
 Dados de usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade é implementado da seguinte maneira:  
  
-   TDE e dados de usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade são desativados por padrão. As instruções não serão automaticamente mascaradas se a criptografia de banco de dados não está habilitada no dispositivo.  
  
-   Habilitando a TDE no dispositivo automaticamente ativa o mascaramento de dados do usuário em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade.  
  
-   Desabilitando a TDE não afeta os dados de usuário de mascaramento no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] os logs de atividade.  
  
-   Você pode habilitar explicitamente de mascaramento de dados de usuário [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logs de atividade usando o **sp_pdw_log_user_data_masking** procedimento.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** função de banco de dados fixa ou **CONTROL SERVER** permissão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir permite que os dados de usuário de log TDE de mascaramento no dispositivo.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
