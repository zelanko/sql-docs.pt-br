---
title: sp_table_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e8695c847e6c5efce1869d55ec68e17bdee5800
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537208"
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Retorna informações de número de linhas e soma de verificação em uma tabela ou exibição indexada, ou compara as informações de número de linhas e soma de verificação com a tabela ou exibição indexada. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura. *Não há suportada para Publicadores Oracle*.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @table = ] 'table'` É o nome da tabela. *tabela* está **sysname**, sem padrão.  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` Especifica se deve retornar o número esperado de linhas na tabela. *expected_rowcount* está **int**, com um padrão NULL. Se for NULL, o número de linhas atual será retornado como um parâmetro de saída. Se um valor for fornecido, esse valor será verificado no número de linhas atual para identificar qualquer diferença.  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` Especifica se deve retornar a soma de verificação esperada para a tabela. *expected_checksum* está **numérico**, com um padrão NULL. Se for NULL, a soma de verificação atual será retornada como um parâmetro de saída. Se um valor for fornecido, esse valor será verificado na soma de verificação atual para identificar qualquer diferença.  
  
`[ @rowcount_only = ] type_of_check_requested` Especifica o tipo de soma de verificação ou número de linhas para executar. *type_of_check_requested* está **smallint**, com um padrão de **1**.  
  
 Se **0**, execute um número de linhas e uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] soma de verificação compatível com 7.0.  
  
 Se **1**, executar apenas uma verificação de número de linhas.  
  
 Se **2**, executar uma soma de verificação do número de linhas e binário.  
  
`[ @owner = ] 'owner'` É o nome do proprietário da tabela. *proprietário* está **sysname**, com um padrão NULL.  
  
`[ @full_or_fast = ] full_or_fast` O método é usado para calcular o número de linhas. *full_or_fast* está **tinyint**, com um padrão de **2**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Efetua contagem completa usando COUNT (*).|  
|**1**|Efetua contagem rápida de **sysindexes**. Contagem de linhas em **sysindexes** é muito mais rápido do que contar linhas na tabela atual. No entanto, porque **sysindexes** é lentamente atualizado, o número de linhas pode não ser preciso.|  
|**2** (padrão)|Efetua contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
`[ @shutdown_agent = ] shutdown_agent` Se o Distribution Agent estiver executando **sp_table_validation**, especifica se o Distribution Agent deve ser desligado imediatamente após a conclusão da validação. *shutdown_agent* está **bit**, com um padrão de **0**. Se **0**, o agente de replicação não desligará. Se **1**, erro 20578 será gerado e o agente de replicação será sinalizado para desligar. Esse parâmetro é ignorado quando **sp_table_validation** é executado diretamente por um usuário.  
  
`[ @table_name = ] table_name` É o nome da tabela da exibição usado para mensagens de saída. *table_name* está **sysname**, com um padrão de **@table**.  
  
`[ @column_list = ] 'column_list'` É a lista de colunas que devem ser usados na função de soma de verificação. *column_list* está **nvarchar (4000)**, com um padrão NULL. Habilita validação de artigos de mesclagem para especificar uma lista de colunas que exclui colunas computadas e colunas de carimbo de data e hora.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Se executar uma validação de soma de verificação e a soma de verificação esperada for igual a soma de verificação na tabela, **sp_table_validation** retorna uma mensagem de que a tabela passou na validação de soma de verificação. Caso contrário, retornará uma mensagem de que a tabela pode estar fora de sincronização e informará a diferença entre o número de linhas esperado e o atual.  
  
 Se executar uma validação de número de linhas e o número esperado de linhas é igual ao número na tabela, **sp_table_validation** retorna uma mensagem de que a tabela passou na validação. Caso contrário, retornará uma mensagem de que a tabela pode estar fora de sincronização e informará a diferença entre o número de linhas esperado e o atual.  
  
## <a name="remarks"></a>Comentários  
 **sp_table_validation** é usado em todos os tipos de replicação. **sp_table_validation** não há suporte para Publicadores Oracle.  
  
 A soma de verificação computa uma CRC (verificação e redundância cíclica) de 32 bits em toda a imagem de linha na página. Ela não verifica colunas seletivamente e não pode operar em uma exibição ou em uma partição vertical da tabela. Além disso, a soma de verificação ignora o conteúdo das **texto** e **imagem** colunas (por design).  
  
 Ao efetuar uma soma de verificação, a estrutura da tabela deve ser idêntica entre os dois servidores; ou seja, as tabelas devem ter as mesmas colunas, na mesma ordem, o mesmo tipo de dados e comprimentos e as mesmas condições NULL/NOT NULL. Por exemplo, se o Publicador tiver executado um CREATE TABLE, depois um ALTER TABLE para adicionar colunas, mas o script aplicado ao Assinante for uma simples tabela CREATE, a estrutura não será a mesma. Se não tiver certeza de que a estrutura das duas tabelas é idêntica, examine [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) e confirme se o deslocamento em cada tabela é o mesmo.  
  
 Valores de ponto flutuante têm probabilidade de gerar as diferenças de soma de verificação se o modo de caractere **bcp** tiver sido usado, que é o caso se a publicação tiver não - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes. Isso se deve a diferenças menores e inevitáveis na precisão ao efetuar conversão para e do modo de caractere.  
  
## <a name="permissions"></a>Permissões  
 Para executar **sp_table_validation**, você deve ter permissões SELECT na tabela que está sendo validada.  
  
## <a name="see-also"></a>Consulte também  
 [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
