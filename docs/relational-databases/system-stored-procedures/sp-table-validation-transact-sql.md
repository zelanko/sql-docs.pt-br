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
ms.openlocfilehash: 736b4f00e8d33a6bd1e095addc5219fe305ae26a
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72173554"
---
# <a name="sp_table_validation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Retorna informações de número de linhas e soma de verificação em uma tabela ou exibição indexada, ou compara as informações de número de linhas e soma de verificação com a tabela ou exibição indexada. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura. *Não há suporte para Publicadores Oracle*.  
  
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
`[ @table = ] 'table'` é o nome da tabela. a *tabela* é **sysname**, sem padrão.  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` especifica se o número esperado de linhas na tabela deve ser retornado. *expected_rowcount* é **int**, com um padrão de NULL. Se for NULL, o número de linhas atual será retornado como um parâmetro de saída. Se um valor for fornecido, esse valor será verificado no número de linhas atual para identificar qualquer diferença.  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` especifica se a soma de verificação esperada deve ser retornada para a tabela. *expected_checksum* é **numérico**, com um padrão de NULL. Se for NULL, a soma de verificação atual será retornada como um parâmetro de saída. Se um valor for fornecido, esse valor será verificado na soma de verificação atual para identificar qualquer diferença.  
  
`[ @rowcount_only = ] type_of_check_requested` especifica o tipo de soma de verificação ou o número de linhas a ser executado. *type_of_check_requested* é **smallint**, com um padrão de **1**.  
  
 Se **0**, execute um número de linhas e uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] soma de verificação compatível com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0.  
  
 Se **1**, execute apenas uma verificação de número de linhas.  
  
 Se **2**, execute um número de linhas e uma soma de verificação binária.  
  
`[ @owner = ] 'owner'` é o nome do proprietário da tabela. *Owner* é **sysname**, com um padrão de NULL.  
  
`[ @full_or_fast = ] full_or_fast` é o método usado para calcular o número de linhas. *full_or_fast* é **tinyint**, com um padrão de **2**, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Efetua contagem completa usando COUNT (*).|  
|**1**|A contagem rápida de **sysindexes. Rows**. A contagem de linhas em **sysindexes** é muito mais rápida do que contar linhas na tabela real. No entanto, como **sysindexes** é atualizado lentamente, o número de linhas pode não ser preciso.|  
|**2** (padrão)|Efetua contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, uma contagem completa (*) sempre será usada.|  
  
`[ @shutdown_agent = ] shutdown_agent` se a Agente de Distribuição estiver executando **sp_table_validation**, especifica se o agente de distribuição deve desligar imediatamente após a conclusão da validação. *shutdown_agent* é **bit**, com um padrão de **0**. Se for **0**, o agente de replicação não será desligado. Se **1**, o erro 20578 é gerado e o agente de replicação é sinalizado para desligar. Esse parâmetro é ignorado quando **sp_table_validation** é executado diretamente por um usuário.  
  
`[ @table_name = ] table_name` é o nome da tabela do modo de exibição usado para mensagens de saída. *table_name* é **sysname**, com um padrão de **\@tabela**.  
  
`[ @column_list = ] 'column_list'` é a lista de colunas que devem ser usadas na função de soma de verificação. *column_list* é **nvarchar (4000)** , com um padrão de NULL. Habilita validação de artigos de mesclagem para especificar uma lista de colunas que exclui colunas computadas e colunas de carimbo de data e hora.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Se executar uma validação de soma de verificação e a soma de verificação esperada for igual à soma de verificação na tabela, **sp_table_validation** retornará uma mensagem de que a tabela passou na validação da soma de verificação. Caso contrário, retornará uma mensagem de que a tabela pode estar fora de sincronização e informará a diferença entre o número de linhas esperado e o atual.  
  
 Se estiver executando uma validação de RowCount e o número esperado de linhas for igual ao número na tabela, **sp_table_validation** retornará uma mensagem informando que a tabela passou na validação da contagem de linhas. Caso contrário, retornará uma mensagem de que a tabela pode estar fora de sincronização e informará a diferença entre o número de linhas esperado e o atual.  
  
## <a name="remarks"></a>Remarks  
 **sp_table_validation** é usado em todos os tipos de replicação. Não há suporte para **sp_table_validation** para Publicadores Oracle.  
  
 A soma de verificação computa uma CRC (verificação e redundância cíclica) de 32 bits em toda a imagem de linha na página. Ela não verifica colunas seletivamente e não pode operar em uma exibição ou em uma partição vertical da tabela. Além disso, a soma de verificação ignora o conteúdo das colunas **Text** e **Image** (por Design).  
  
 Ao efetuar uma soma de verificação, a estrutura da tabela deve ser idêntica entre os dois servidores; ou seja, as tabelas devem ter as mesmas colunas, na mesma ordem, o mesmo tipo de dados e comprimentos e as mesmas condições NULL/NOT NULL. Por exemplo, se o Publicador tiver executado um CREATE TABLE, depois um ALTER TABLE para adicionar colunas, mas o script aplicado ao Assinante for uma simples tabela CREATE, a estrutura não será a mesma. Se você não tiver certeza de que a estrutura das duas tabelas é idêntica, examine [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) e confirme se o deslocamento em cada tabela é o mesmo.  
  
 Os valores de ponto flutuante provavelmente gerarão diferenças de soma de verificação se o **bcp** de modo de caractere tiver sido usado, que é o caso se a publicação tiver Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso se deve a diferenças menores e inevitáveis na precisão ao efetuar conversão para e do modo de caractere.  
  
## <a name="permissions"></a>Permissões  
 Para executar **sp_table_validation**, você deve ter permissões SELECT na tabela que está sendo validada.  
  
## <a name="see-also"></a>Consulte também  
 [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
