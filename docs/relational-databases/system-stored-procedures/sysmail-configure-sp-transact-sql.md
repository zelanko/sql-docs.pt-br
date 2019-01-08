---
title: sysmail_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe47df497b61d35c66bfebfb3ba5a75fad0e183
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588550"
---
# <a name="sysmailconfiguresp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera definições de configuração do Database Mail. As definições de configuração especificadas com **sysmail_configure_sp** se aplicam a todo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@parameter_name** =] **'**_parameter_name_**'**  
 O nome do parâmetro a ser alterado.  
  
 [**@parameter_value** =] **'**_parameter_value_**'**  
 O novo valor do parâmetro.  
  
 [**@description** =] **'**_descrição_**'**  
 Uma descrição do parâmetro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 O Database Mail usa os seguintes parâmetros:  
  
||||  
|-|-|-|  
|Nome do parâmetro|Descrição|Valor Padrão|  
|*AccountRetryAttempts*|O número de vezes que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado.|**1**|  
|*AccountRetryDelay*|O período de tempo, em segundos, que o processo de email externo deve esperar entre tentativas de envio de uma mensagem.|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|O período mínimo de tempo, em segundos, que o processo de email externo permanece ativo. Quando o Database Mail estiver enviando muitas mensagens, aumente este valor para manter o Database Mail ativo e evitar a sobrecarga de inícios e paradas frequentes.|**600**|  
|*DefaultAttachmentEncoding*|A codificação padrão para anexos de email.|MIME|  
|*MaxFileSize*|O tamanho máximo de um anexo, em bytes.|**1000000**|  
|*ProhibitedExtensions*|Uma lista separada por vírgula de extensões que não podem ser enviadas como um anexo a uma mensagem de email.|**exe, dll, vbs, js**|  
|*LoggingLevel*|Especifique quais mensagens são registradas no log do Database Mail. Um dos seguintes valores numéricos:<br /><br /> 1 - Este é o modo normal. Registra apenas erros.<br /><br /> 2 - Este é o modo estendido. Registra erros, avisos e mensagens informativas.<br /><br /> 3 - Este é o modo detalhado. Registra erros, avisos, mensagens informativas, mensagens de êxito e mensagens internas adicionais. Use este modo para diagnóstico.|**2**|  
  
 O procedimento armazenado **sysmail_configure_sp** está no **msdb** banco de dados e é de propriedade de **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão os membros de **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Definindo o Database Mail para repetir cada conta 10 vezes**  
  
 O exemplo a seguir mostra a definição do Database Mail para repetir cada conta dez vezes antes de considerá-la inacessível.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B. Definindo o tamanho máximo do anexo como dois megabytes**  
  
 O exemplo a seguir mostra a definição do tamanho máximo do anexo como 2 megabytes.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
