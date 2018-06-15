---
title: sp_trace_generateevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 398fb058ae7be57cf0c26b26e77d6e82aafd0df3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260652"
---
# <a name="sptracegenerateevent-transact-sql"></a>sp_trace_generateevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um evento definido pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**Observação:** esse procedimento armazenado é **não** preterido. Todos os outros procedimentos armazenados relacionados a rastreamento são substituídos.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@eventid=**] *event_id*  
 É a ID do evento a ser ativado. *event_id* é **int**, sem padrão. A ID deve ser um dos números de evento de 82 a 91, que representam eventos definidos pelo usuário conforme definido com [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
 [ **@userinfo**= ] **'***user_info***'**  
 É a cadeia de caracteres opcional definida pelo usuário que identifica o motivo do evento. *user_info* é **nvarchar (128)**, com um padrão NULL.  
  
 [ **@userdata**=] *user_data*  
 São os dados opcionais especificados pelo usuário para o evento. *user_data* é **varbinary (8000)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 A tabela a seguir descreve os valores de código que os usuários podem obter após a conclusão do procedimento armazenado.  
  
|Código de retorno|Description|  
|-----------------|-----------------|  
|**0**|Nenhum erro.|  
|**1**|Erro desconhecido.|  
|**3**|O evento especificado não é válido. O evento pode não existir ou não é um apropriado para o procedimento de loja.|  
|**13**|Memória insuficiente. Retornado quando não há memória suficiente para executar a ação especificada.|  
  
## <a name="remarks"></a>Remarks  
 **sp_trace_generateevent** executa muitas das ações anteriormente executadas pelo **xp_trace _\***  procedimentos armazenados estendidos. Use **sp_trace_generateevent** em vez de **xp_trace_generate_event**.  
  
 Somente os números de IDs de eventos definidos pelo usuário podem ser usados com **sp_trace_generateevent**. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá gerar um erro se outros números de ID do evento forem usados.  
  
 Os parâmetros de rastreamento de SQL todos os procedimentos armazenados (**sp_trace_xx**) são rigorosamente tipados. Se esses parâmetros não forem chamados com os tipos de dados com parâmetro de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER TRACE.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um evento configurável pelo usuário em uma tabela de exemplo.  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
