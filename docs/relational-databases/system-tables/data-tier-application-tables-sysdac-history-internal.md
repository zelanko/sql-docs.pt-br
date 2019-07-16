---
title: sysdac_history_internal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc058fea8e2ce86584c19a7a93018734f4782f69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084760"
---
# <a name="data-tier-application-tables---sysdachistoryinternal"></a>Tabelas de aplicativo da camada de dados – sysdac_history_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre as ações realizadas para gerenciar aplicativos da camada de dados (DAC). Essa tabela é armazenada na **dbo** esquema da **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|Identificador da ação|  
|**sequence_id**|**int**|Identifica uma etapa dentro de uma ação.|  
|**instance_id**|**uniqueidentifier**|Identificador da instância do DAC. Esta coluna pode ser unida a **instance_id** coluna em [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md).|  
|**action_type**|**tinyint**|Identificador do tipo da ação:<br /><br /> **0** = implantar<br /><br /> **1** = criar<br /><br /> **2** = renomear<br /><br /> **3** = detach<br /><br /> **4** = excluir|  
|**action_type_name**|**varchar(19)**|Nome do tipo de ação.<br /><br /> **deploy**<br /><br /> **create**<br /><br /> **rename**<br /><br /> **detach**<br /><br /> **delete**|  
|**dac_object_type**|**tinyint**|Identificador do tipo de objeto afetado pela ação:<br /><br /> **0** = dacpac<br /><br /> **1** = logon<br /><br /> **2** = banco de dados|  
|**dac_object_type_name**|**varchar(8)**|Nome do tipo de objeto afetado pela ação:<br /><br /> **dacpac** = instância do DAC<br /><br /> **login**<br /><br /> **banco de dados**|  
|**action_status**|**tinyint**|Código que identifica o status atual da ação:<br /><br /> **0** = pendente<br /><br /> **1** = êxito<br /><br /> **2** = falha|  
|**action_status_name**|**varchar(11)**|Status atual da ação:<br /><br /> **Pendente**<br /><br /> **Sucesso**<br /><br /> **fail**|  
|**Necessária**|**bit**|Usada pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ao reverter uma operação de DAC.|  
|**dac_object_name_pretran**|**sysname**|Nome do objeto antes que a transação que contém a ação seja confirmada. Usado somente para bancos de dados e logons.|  
|**dac_object_name_posttran**|**sysname**|Nome do objeto depois que a transação que contém a ação seja confirmada. Usado somente para bancos de dados e logons.|  
|**sqlscript**|**nvarchar(max)**|Script [!INCLUDE[tsql](../../includes/tsql-md.md)] que implementa uma ação em um banco de dados ou logon.|  
|**payload**|**varbinary(max)**|Definição de pacote do DAC salva em uma cadeia de caracteres codificada binária.|  
|**Comentários**|**varchar(max)**|Registra o logon de um usuário que aceitou perda de dados potencial em uma atualização de DAC.|  
|**error_string**|**nvarchar(max)**|Mensagem de erro gerada se a ação encontrar um erro.|  
|**created_by**|**sysname**|O logon que iniciou a ação que criou essa entrada.|  
|**date_created**|**datetime**|A data e a hora de criação dessa entrada.|  
|**date_modified**|**datetime**|A data e a hora da última alteração feita na entrada.|  
  
## <a name="remarks"></a>Comentários  
 As ações de gerenciamento do DAC, como implantar ou excluir um DAC, geram várias etapas. Cada ação é atribuída um identificador de ação. Cada etapa é atribuída um número de sequência e uma linha na **sysdac_history_internal**, em que o status da etapa é registrado. Cada linha é criada quando inicia a etapa de ação e é atualizada para refletir o status da operação quando necessário. Por exemplo, uma ação de implantação do DAC pode ser atribuída **action_id** 12 e pode obter quatro linhas em **sysdac_history_internal**:  
  
|||||  
|-|-|-|-|  
|**action_id**|**sequence_id**|**action_type_name**|**dac_object_type_name**|  
|12|0|criar|dacpac|  
|12|1|criar|Logon|  
|12|2|criar|database|  
|12|3|renomear|database|  
  
 Operações de DAC, como delete remove linhas de **sysdac_history_internal**. Você pode usar a seguinte consulta para excluir manualmente as linhas dos DACs que não são mais implantados em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
```sql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 A exclusão das linhas dos DACs ativos não impacta as operações DAC; o único impacto é que você não conseguirá reportar o histórico completo do DAC.  
  
> [!NOTE]  
>  Atualmente, não há nenhum mecanismo para a exclusão **sysdac_history_internal** linhas em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin. Acesso somente leitura a essa exibição está disponível para todos os usuários com permissões para se conectar ao banco de dados mestre.  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 [sysdac_instances_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
