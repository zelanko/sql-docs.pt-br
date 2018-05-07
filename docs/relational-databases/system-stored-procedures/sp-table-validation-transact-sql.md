---
title: sp_table_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d82517f09ad18c7cc0b2e8d49acfdae6ab200ee9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Retorna informações de número de linhas e soma de verificação em uma tabela ou exibição indexada, ou compara as informações de número de linhas e soma de verificação com a tabela ou exibição indexada. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação e no Assinante, no banco de dados de assinatura. *Não há suportada para editores Oracle*.  
  
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
 [  **@table=**] **'***tabela***'**  
 É o nome da tabela. *tabela* é **sysname**, sem padrão.  
  
 [  **@expected_rowcount=**] *expected_rowcount*saída  
 Especifica se o número de linhas esperado na tabela deve ser retornado. *expected_rowcount* é **int**, com um padrão NULL. Se for NULL, o número de linhas atual será retornado como um parâmetro de saída. Se um valor for fornecido, esse valor será verificado no número de linhas atual para identificar qualquer diferença.  
  
 [  **@expected_checksum=**] *expected_checksum*saída  
 Especifica se a soma de verificação esperada da tabela deve ser retornada. *expected_checksum* é **numérico**, com um padrão NULL. Se for NULL, a soma de verificação atual será retornada como um parâmetro de saída. Se um valor for fornecido, esse valor será verificado na soma de verificação atual para identificar qualquer diferença.  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 Especifica o tipo de soma de verificação ou contagem de linhas a ser executada. *type_of_check_requested* é **smallint**, com um padrão de **1**.  
  
 Se **0**, executar um número de linhas e um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] soma de verificação compatível com 7.0.  
  
 Se **1**, executar uma verificação de número de linhas apenas.  
  
 Se **2**, executar uma soma de verificação do número de linhas e binário.  
  
 [  **@owner=**] **'***proprietário***'**  
 É o nome do proprietário da tabela. *proprietário* é **sysname**, com um padrão NULL.  
  
 [  **@full_or_fast=**] *full_or_fast*  
 É o método usado para calcular a contagem de linhas. *full_or_fast* é **tinyint**, com um padrão de **2**, e pode ser um destes valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Efetua contagem completa usando COUNT (*).|  
|**1**|Efetua contagem rápida de **sysindexes**. Contagem de linhas em **sysindexes** é muito mais rápido do que contar linhas na tabela atual. No entanto, como **sysindexes** lentamente é atualizado, o número de linhas pode não ser preciso.|  
|**2** (padrão)|Efetua contagem rápida condicional tentando primeiro o método rápido. Se o método rápido mostrar diferenças, reverterá ao método completo. Se *expected_rowcount* for NULL e o procedimento armazenado estiver sendo usado para obter o valor, um COUNT(*) completo sempre será usado.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Se estiver executando o agente de distribuição **sp_table_validation**, especifica se o agente de distribuição deve ser desligado imediatamente após a conclusão da validação. *shutdown_agent* é **bit**, com um padrão de **0**. Se **0**, o agente de replicação não é desligado. Se **1**, erro 20578 será gerado e o agente de replicação é sinalizado para desligar. Esse parâmetro é ignorado quando **sp_table_validation** é executado diretamente por um usuário.  
  
 [  **@table_name =**] *table_name*  
 É o nome da tabela da exibição usada para mensagens de saída. *table_name* é **sysname**, com um padrão de **@table**.  
  
 [ **@column_list**=] **'***column_list***'**  
 É a lista de colunas que devem ser usadas na função soma de verificação. *column_list* é **nvarchar (4000)**, com um padrão NULL. Habilita validação de artigos de mesclagem para especificar uma lista de colunas que exclui colunas computadas e colunas de carimbo de data e hora.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Se executar uma validação de soma de verificação e a soma de verificação esperada é igual a soma de verificação na tabela, **sp_table_validation** retorna uma mensagem de que a tabela passou na validação de soma de verificação. Caso contrário, retornará uma mensagem de que a tabela pode estar fora de sincronização e informará a diferença entre o número de linhas esperado e o atual.  
  
 Se executar uma validação de número de linhas e o número esperado de linhas é igual ao número na tabela, **sp_table_validation** retorna uma mensagem de que a tabela passou na validação. Caso contrário, retornará uma mensagem de que a tabela pode estar fora de sincronização e informará a diferença entre o número de linhas esperado e o atual.  
  
## <a name="remarks"></a>Remarks  
 **sp_table_validation** é usado em todos os tipos de replicação. **sp_table_validation** não há suporte para editores Oracle.  
  
 A soma de verificação computa uma CRC (verificação e redundância cíclica) de 32 bits em toda a imagem de linha na página. Ela não verifica colunas seletivamente e não pode operar em uma exibição ou em uma partição vertical da tabela. Além disso, a soma de verificação ignora o conteúdo de **texto** e **imagem** colunas (por padrão).  
  
 Ao efetuar uma soma de verificação, a estrutura da tabela deve ser idêntica entre os dois servidores; ou seja, as tabelas devem ter as mesmas colunas, na mesma ordem, o mesmo tipo de dados e comprimentos e as mesmas condições NULL/NOT NULL. Por exemplo, se o Publicador tiver executado um CREATE TABLE, depois um ALTER TABLE para adicionar colunas, mas o script aplicado ao Assinante for uma simples tabela CREATE, a estrutura não será a mesma. Se não tiver certeza de que a estrutura das duas tabelas é idêntica, examine [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) e confirme se o deslocamento em cada tabela é o mesmo.  
  
 Valores de ponto flutuante têm probabilidade de gerar diferenças de soma de verificação se o modo de caractere **bcp** foi usado, que é o caso se a publicação não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes. Isso se deve a diferenças menores e inevitáveis na precisão ao efetuar conversão para e do modo de caractere.  
  
## <a name="permissions"></a>Permissões  
 Para executar **sp_table_validation**, você deve ter permissões SELECT na tabela que está sendo validada.  
  
## <a name="see-also"></a>Consulte também  
 [Soma de verificação &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
