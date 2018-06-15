---
title: sp_configure (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 05074a051f39e8b2dd81314ed6e230868c410c49
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239966"
---
# <a name="spconfigure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/t-sql-appliesto-ss-asdbmi-xxxx-pwd-md.md)]

  Exibe ou altera parâmetros de configuração global para o servidor atual.

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
> [!NOTE]  
>  Opções de configuração de nível de banco de dados, consulte [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar o NUMA, consulte [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
sp_configure [ [ @configname = ] 'option_name'   
    [ , [ @configvalue = ] 'value' ] ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
-- List all of the configuration options  
sp_configure  
[;]  
  
-- Configure Hadoop connectivity  
sp_configure [ @configname= ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@configname=** ] **'***option_name***'**  
 É o nome de uma opção de configuração. *option_name* é **varchar(35)**, com um padrão de NULL. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] reconhece qualquer cadeia de caracteres única que faça parte do nome de configuração. Se não for especificado, a lista completa de opções será retornada.  
  
 Para obter informações sobre as opções de configuração disponíveis e suas configurações, consulte [opções de configuração de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 [ **@configvalue=** ] **'***value***'**  
 É a nova definição de configuração. *value* é **int**, com um padrão NULL. O valor máximo depende da opção individual.  
  
 Para ver o valor máximo para cada opção, consulte o **máximo** coluna o **Configurations** exibição do catálogo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando executado sem parâmetros, **sp_configure** retorna um conjunto de resultados com cinco colunas e ordena as opções alfabeticamente em ordem crescente, conforme mostrado na tabela a seguir.  
  
 Os valores para **config_value** e **run_value** não são automaticamente equivalentes. Depois de atualizar uma definição de configuração usando **sp_configure**, o administrador do sistema deve atualizar o valor de configuração usando RECONFIGURE ou RECONFIGURE WITH OVERRIDE. Para obter mais informações, consulte a seção Comentários.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|O nome da opção de configuração.|  
|**minimum**|**Int**|Valor mínimo da opção de configuração.|  
|**maximum**|**Int**|Valor máximo da opção de configuração.|  
|**config_value**|**Int**|Valor para o qual a opção de configuração foi definida usando **sp_configure** (valor em **Configurations**). Para obter mais informações sobre essas opções, consulte [opções de configuração de servidor &#40;SQL Server&#41; ](../../database-engine/configure-windows/server-configuration-options-sql-server.md) e [Configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
|**run_value**|**Int**|Valor da opção de configuração em execução no momento (valor em **value_in_use**).<br /><br /> Para obter mais informações, consulte [Configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
  
## <a name="remarks"></a>Remarks  
 Use **sp_configure** para exibir ou alterar as configurações de nível de servidor. Para alterar configurações de nível de banco de dados, use ALTER DATABASE. Para alterar configurações que afetam somente a sessão do usuário atual, use a instrução SET.  
  
## <a name="updating-the-running-configuration-value"></a>Atualizando o valor de configuração de execução  
 Quando você especificar um novo *valor* para um *opção*, o conjunto de resultados mostra este valor no **config_value** coluna. Esse valor difere inicialmente o valor de **run_value** coluna, que mostra o valor de configuração em execução no momento. Para atualizar o valor de configuração em execução no **run_value** coluna, o administrador do sistema deve executar RECONFIGURE ou RECONFIGURE WITH OVERRIDE.  
  
 RECONFIGURE e RECONFIGURE WITH OVERRIDE trabalham com todas opções de configuração. Porém, a instrução básica RECONFIGURE rejeita qualquer valor de opção que está fora de um intervalo razoável, pois caso contrário isso pode causar conflitos entre opções. Por exemplo, RECONFIGURE irá gerar um erro se o **intervalo de recuperação** valor for maior que 60 minutos ou se o **máscara de afinidade** valor se sobrepõe a **máscara de afinidade de e/s**valor. RECONFIGURE WITH OVERRIDE, ao contrário, aceita qualquer valor de opção com o tipo de dados correto e força a reconfiguração com o valor especificado.  
  
> [!CAUTION]  
>  Um valor de opção inadequado pode afetar negativamente a configuração da instância do servidor. Use RECONFIGURE WITH OVERRIDE com cuidado.  
  
 A instrução RECONFIGURE atualiza algumas opções dinamicamente, outras opções requerem a parada do servidor e reinicialização. Por exemplo, o **memória mínima do servidor** e **memória máxima do servidor** opções de memória do servidor é atualizado dinamicamente no [!INCLUDE[ssDE](../../includes/ssde-md.md)]; portanto, você pode alterá-los sem reiniciar o servidor. Por outro lado, reconfigurar o valor em execução do **fator de preenchimento** opção requer a reinicialização de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Após executar RECONFIGURE em uma opção de configuração, você pode ver se a opção foi dinamicamente atualizada executando **sp_configure'***option_name***'**. Os valores de **run_value** e **config_value** colunas devem corresponder com uma opção dinamicamente atualizada. Você também pode verificar para ver quais opções são dinâmicas consultando o **is_dynamic** coluna o **Configurations** exibição do catálogo.  
  
> [!NOTE]  
>  Se um especificado *valor* é muito alto para uma opção, o **run_value** coluna reflete o fato de que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] definiu a memória dinâmica em vez de usar uma configuração que não é válida.  
  
 Para obter mais informações, consulte [RECONFIGURAR &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md).  
  
## <a name="advanced-options"></a>Opções Avançadas  
 Algumas opções de configuração, tais como **máscara de afinidade** e **intervalo de recuperação**, são designadas como opções avançadas. Por padrão, essas opções não estão disponíveis para exibição e alteração. Para disponibilizá-los, defina o **ShowAdvancedOptions** opção de configuração para 1.  
  
 Para obter mais informações sobre as opções de configuração e suas configurações, consulte [opções de configuração de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, você deve ter a permissão ALTER SETTINGS nível de servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. Listando as opções de configuração avançada  
 O exemplo a seguir mostra como configurar e listar todas as opções de configuração. Opções de configuração avançada são exibidas pelo primeiro parâmetro `show advanced option` como `1`. Depois que essa opção for alterada, a execução de `sp_configure` sem parâmetros exibe todas as opções de configuração.  
  
```  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 Aqui está a mensagem: "Opção de configuração 'show advanced options' alterada de 0 para 1. Execute a instrução RECONFIGURE para instalar”.  
  
 Execute `RECONFIGURE` e exiba todas as opções de configuração:  
  
```  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. Alterando uma opção de configuração  
 O exemplo a seguir define o `recovery interval` de sistema para `3` minutos.  
  
```  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. Listar todas as configurações disponíveis  
 O exemplo a seguir mostra como listar todas as opções de configuração.  
  
```  
EXEC sp_configure;  
```  
  
 O resultado retorna o nome da opção seguido pelos valores mínimo e máximo da opção. O **config_value** é o valor que [!INCLUDE[ssDW](../../includes/ssdw-md.md)] usará após a reconfiguração. O **run_value** é o valor que está sendo usado. Normalmente, **config_value** e **run_value** são os mesmos, a menos que o valor esteja sendo alterado.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. Listar as definições de configuração de um nome de configuração  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. Definir a conectividade do Hadoop  
 Configuração de conectividade do Hadoop requer algumas etapas mais além de executar sp_configure. Para obter o procedimento completo, consulte [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [RECONFIGURE & #40; Transact-SQL & #41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Opções de configuração do servidor &#40; SQL Server e &#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
