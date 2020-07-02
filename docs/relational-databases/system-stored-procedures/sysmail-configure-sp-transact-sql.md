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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8e3ca89ab5974dbe53b12a2b5b369958ab38755c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720161"
---
# <a name="sysmail_configure_sp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Altera definições de configuração do Database Mail. As definições de configuração especificadas com **sysmail_configure_sp** se aplicam à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância inteira.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@parameter_name** =] **'**_parameter_name_**'**  
 O nome do parâmetro a ser alterado.  
  
 [ **@parameter_value** =] **'**_parameter_value_**'**  
 O novo valor do parâmetro.  
  
 [ **@description** =] **'**_Descrição_**'**  
 Uma descrição do parâmetro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O Database Mail usa os seguintes parâmetros:  
  
||||  
|-|-|-|  
|Nome do parâmetro|Descrição|Valor Padrão|  
|*AccountRetryAttempts*|O número de vezes que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado.|**1**|  
|*AccountRetryDelay*|O período de tempo, em segundos, que o processo de email externo deve esperar entre tentativas de envio de uma mensagem.|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|O período mínimo de tempo, em segundos, que o processo de email externo permanece ativo. Quando o Database Mail estiver enviando muitas mensagens, aumente este valor para manter o Database Mail ativo e evitar a sobrecarga de inícios e paradas frequentes.|**600**|  
|*DefaultAttachmentEncoding*|A codificação padrão para anexos de email.|MIME|  
|*MaxFileSize*|O tamanho máximo de um anexo, em bytes.|**1 milhão**|  
|*ProhibitedExtensions*|Uma lista separada por vírgula de extensões que não podem ser enviadas como um anexo a uma mensagem de email.|**exe,dll,vbs,js**|  
|*LoggingLevel*|Especifique quais mensagens são registradas no log do Database Mail. Um dos seguintes valores numéricos:<br /><br /> 1 - Este é o modo normal. Registra apenas erros.<br /><br /> 2 - Este é o modo estendido. Registra erros, avisos e mensagens informativas.<br /><br /> 3 - Este é o modo detalhado. Registra erros, avisos, mensagens informativas, mensagens de êxito e mensagens internas adicionais. Use este modo para diagnóstico.|**2**|  
  
 O procedimento armazenado **sysmail_configure_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [&#41;&#40;Transact-SQL de sysmail_help_configure_sp](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
