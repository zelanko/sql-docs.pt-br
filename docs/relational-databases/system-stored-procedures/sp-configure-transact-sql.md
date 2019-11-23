---
title: sp_configure (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_configure
- sp_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_configure
ms.assetid: d18b251d-b37a-4f5f-b50c-502d689594c8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 09f5a26493600fd346192f6ba7ebbc73ea7ed184
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536213"
---
# <a name="sp_configure-transact-sql"></a>sp_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-pdw-md.md)]

  Exibe ou altera parâmetros de configuração global para o servidor atual.

> [!NOTE]  
> Para obter opções de configuração no nível do banco de dados, consulte [ALTER DATABASE scopeed Configuration &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). Para configurar o soft-NUMA, consulte [Soft- &#40;numa&#41;SQL Server](../../database-engine/configure-windows/soft-numa-sql-server.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @configname = ] 'option_name'` é o nome de uma opção de configuração. *option_name* é **varchar(35)** , com um padrão de NULL. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] reconhece qualquer cadeia de caracteres única que faça parte do nome de configuração. Se não for especificado, a lista completa de opções será retornada.  
  
 Para obter informações sobre as opções de configuração disponíveis e suas configurações, consulte [opções &#40;de&#41;configuração do servidor SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
`[ @configvalue = ] 'value'` é a nova definição de configuração. *value* é **int**, com um padrão NULL. O valor máximo depende da opção individual.  
  
 Para ver o valor máximo de cada opção, consulte a coluna **máximo** da exibição do catálogo **Sys. Configurations** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando executado sem parâmetros, **sp_configure** retorna um conjunto de resultados com cinco colunas e ordena as opções alfabeticamente em ordem crescente, conforme mostrado na tabela a seguir.  
  
 Os valores para **config_value** e **run_value** não são equivalentes automaticamente. Depois de atualizar uma definição de configuração usando **sp_configure**, o administrador do sistema deve atualizar o valor de configuração em execução usando RECONFIGURE ou RECONFIGURE com override. Para obter mais informações, consulte a seção Comentários.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|O nome da opção de configuração.|  
|**minimum**|**int**|Valor mínimo da opção de configuração.|  
|**maximum**|**int**|Valor máximo da opção de configuração.|  
|**config_value**|**int**|Valor para o qual a opção de configuração foi definida usando **sp_configure** (valor em **Sys. Configurations. Value**). Para obter mais informações sobre essas opções, consulte [opções &#40;de configuração&#41; do servidor SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md) e [ &#40;sys. Configurations Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
|**run_value**|**int**|Valor em execução no momento da opção de configuração (valor em **Sys. Configurations. value_in_use**).<br /><br /> Para obter mais informações, consulte [Sys. &#40;Configurations&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md).|  
  
## <a name="remarks"></a>Remarks  
 Use **sp_configure** para exibir ou alterar as configurações de nível de servidor. Para alterar configurações de nível de banco de dados, use ALTER DATABASE. Para alterar configurações que afetam somente a sessão do usuário atual, use a instrução SET.  
  
### [!INCLUDE [ssbigdataclusters-ss-nover](../../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE [big-data-clusters-master-instance-ha-endpoint-requirement](../../includes/big-data-clusters-master-instance-ha-endpoint-requirement.md)]

## <a name="updating-the-running-configuration-value"></a>Atualizando o valor de configuração de execução  
 Quando você especifica um novo *valor* para uma *opção*, o conjunto de resultados mostra esse valor na coluna **config_value** . Esse valor é, inicialmente, diferente do valor na coluna **run_value** , que mostra o valor de configuração em execução no momento. Para atualizar o valor de configuração em execução na coluna **run_value** , o administrador do sistema deve executar a reconfiguração ou reconfigurar com override.  
  
 RECONFIGURE e RECONFIGURE WITH OVERRIDE trabalham com todas opções de configuração. Porém, a instrução básica RECONFIGURE rejeita qualquer valor de opção que está fora de um intervalo razoável, pois caso contrário isso pode causar conflitos entre opções. Por exemplo, reconfigure gera um erro se o valor do **intervalo de recuperação** for maior que 60 minutos ou se o valor da **máscara de afinidade** se sobrepor ao valor de **máscara de e/s de afinidade** . RECONFIGURE WITH OVERRIDE, ao contrário, aceita qualquer valor de opção com o tipo de dados correto e força a reconfiguração com o valor especificado.  
  
> [!CAUTION]  
> Um valor de opção inadequado pode afetar negativamente a configuração da instância do servidor. Use RECONFIGURE WITH OVERRIDE com cuidado.  
  
 A instrução RECONFIGURE atualiza algumas opções dinamicamente, outras opções requerem a parada do servidor e reinicialização. Por exemplo, as opções de memória **mínima** do servidor e memória **máxima** do servidor são atualizadas dinamicamente no [!INCLUDE[ssDE](../../includes/ssde-md.md)]; Portanto, você pode alterá-los sem reiniciar o servidor. Por outro lado, a reconfiguração do valor em execução da opção **fator de preenchimento** requer a reinicialização do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Depois de executar RECONFIGURE em uma opção de configuração, você pode ver se a opção foi atualizada dinamicamente executando **sp_configure '***option_name***'** . Os valores nas colunas **run_value** e **config_value** devem corresponder a uma opção atualizada dinamicamente. Você também pode verificar para ver quais opções são dinâmicas examinando a coluna **is_dynamic** da exibição do catálogo **Sys. Configurations** .  
 
 A alteração também é gravada no log de erros do SQL Server.
  
> [!NOTE]  
>  Se um *valor* especificado for muito alto para uma opção, a coluna **run_value** refletirá o fato de que a [!INCLUDE[ssDE](../../includes/ssde-md.md)] tem como padrão a memória dinâmica, em vez de usar uma configuração que não seja válida.  
  
 Para obter mais informações, consulte [reconfigure &#40;Transact-&#41;SQL](../../t-sql/language-elements/reconfigure-transact-sql.md).  
  
## <a name="advanced-options"></a>Opções Avançadas  
 Algumas opções de configuração, como a **máscara de afinidade** e o intervalo de **recuperação**, são designadas como opções avançadas. Por padrão, essas opções não estão disponíveis para exibição e alteração. Para torná-los disponíveis, defina a opção de configuração de **Imadvancedoptions** como 1.  
  
 Para obter mais informações sobre as opções de configuração e suas configurações, consulte [opções &#40;de&#41;configuração do servidor SQL Server](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou para executar a instrução RECONFIGURE, você deve receber a permissão de nível de servidor ALTER Settings. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-the-advanced-configuration-options"></a>A. Listando as opções de configuração avançada  
 O exemplo a seguir mostra como configurar e listar todas as opções de configuração. Opções de configuração avançada são exibidas pelo primeiro parâmetro `show advanced option` como `1`. Depois que essa opção for alterada, a execução de `sp_configure` sem parâmetros exibe todas as opções de configuração.  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'show advanced option', '1';  
```  
  
 Aqui está a mensagem: "Opção de configuração 'show advanced options' alterada de 0 para 1. Execute a instrução RECONFIGURE para instalar”.  
  
 Execute `RECONFIGURE` e exiba todas as opções de configuração:  
  
```sql  
RECONFIGURE;  
EXEC sp_configure;  
```  
  
### <a name="b-changing-a-configuration-option"></a>B. Alterando uma opção de configuração  
 O exemplo a seguir define o `recovery interval` de sistema para `3` minutos.  
  
```sql  
USE master;  
GO  
EXEC sp_configure 'recovery interval', '3';  
RECONFIGURE WITH OVERRIDE;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-list-all-available-configuration-settings"></a>C. Listar todas as configurações disponíveis  
 O exemplo a seguir mostra como listar todas as opções de configuração.  
  
```sql  
EXEC sp_configure;  
```  
  
 O resultado retorna o nome da opção seguido pelos valores mínimo e máximo da opção. O **config_value** é o valor que [!INCLUDE[ssDW](../../includes/ssdw-md.md)] será usado quando a reconfiguração for concluída. O **run_value** é o valor que está sendo usado. Normalmente, **config_value** e **run_value** são os mesmos, a menos que o valor esteja sendo alterado.  
  
### <a name="d-list-the-configuration-settings-for-one-configuration-name"></a>D. Listar as definições de configuração de um nome de configuração  
  
```sql  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="e-set-hadoop-connectivity"></a>E. Definir a conectividade do Hadoop  
 A configuração da conectividade do Hadoop requer mais algumas etapas, além da execução de sp_configure. Para obter o procedimento completo, consulte [criar fonte &#40;de dados externa Transact&#41;-SQL](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
