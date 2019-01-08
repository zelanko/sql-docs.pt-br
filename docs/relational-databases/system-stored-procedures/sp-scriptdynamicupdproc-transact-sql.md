---
title: sp_scriptdynamicupdproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptdynamicupdproc_TSQL
- sp_scriptdynamicupdproc
helpviewer_keywords:
- sp_scriptdynamicupdproc
ms.assetid: b4c18863-ed92-4aa2-a04f-7ed832fc9e07
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 65f1990c1c35278e67036f2bb3699f268a2aca8a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751839"
---
# <a name="spscriptdynamicupdproc-transact-sql"></a>sp_scriptdynamicupdproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera a instrução CREATE PROCEDURE que cria um procedimento armazenado de atualização dinâmica. A instrução UPDATE no procedimento armazenado personalizado é criada dinamicamente com base na sintaxe MCALL, que indica quais colunas devem ser alteradas. Use esse procedimento armazenado se o número de índices na tabela de assinaturas estiver aumentando e o número de colunas alteradas for pequeno. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_scriptdynamicupdproc [ @artid =] artid  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@artid=**] *artid*  
 É a ID do artigo. *artid* está **int**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados que consiste em uma única **nvarchar (4000)** coluna. O conjunto de resultados forma a instrução completa CREATE PROCEDURE usada para criar o procedimento armazenado personalizado.  
  
## <a name="remarks"></a>Comentários  
 **sp_scriptdynamicupdproc** é usado em replicação transacional. A lógica de script MCALL padrão inclui todas as colunas da instrução UPDATE e usa um bitmap para determinar as colunas alteradas. Se uma coluna não foi alterada, será redefinida como ela mesma, o que geralmente não causa problemas. Se a coluna for indexada, ocorrerá processamento extra. A abordagem dinâmica só inclui as colunas que foram alteradas, o que fornece uma cadeia de caracteres UPDATE otimizada. Porém, processamento extra incorre em tempo de execução, quando a instrução UPDATE dinâmica é criada. Recomendamos que você teste as abordagens dinâmica e estática e depois escolha a melhor solução.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_scriptdynamicupdproc**.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo cria um artigo (com *artid* definido como **1**) na **autores** na tabela a **pubs** de banco de dados e especifica que a atualização instrução é o procedimento personalizado a ser executado:  
  
```  
'MCALL sp_mupd_authors'  
```  
  
 Gera os procedimentos armazenados personalizados a serem executados pelo Distribution Agent no Assinante, executando o seguinte procedimento armazenado no Publicador:  
  
```  
EXEC sp_scriptdynamicupdproc @artid = '1'  
  
The statement returns:  
  
CREATE PROCEDURE [sp_mupd_authors]   
  @c1 varchar(11),@c2 varchar(40),@c3 varchar(20),@c4 char(12),@c5 varchar(40),@c6 varchar(20),  
  @c7 char(2),@c8 char(5),@c9 bit,@pkc1 varchar(11),@bitmap binary(2)  
as  
  
declare @stmt nvarchar(4000), @spacer nvarchar(1)  
SELECT @spacer =N''  
SELECT @stmt = N'UPDATE [authors] SET '  
  
if substring(@bitmap,1,1) & 2 = 2  
begin  
  select @stmt = @stmt + @spacer + N'[au_lname]' + N'=@2'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 4 = 4  
begin  
  select @stmt = @stmt + @spacer + N'[au_fname]' + N'=@3'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 8 = 8  
begin  
  select @stmt = @stmt + @spacer + N'[phone]' + N'=@4'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 16 = 16  
begin  
  select @stmt = @stmt + @spacer + N'[address]' + N'=@5'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 32 = 32  
begin  
  select @stmt = @stmt + @spacer + N'[city]' + N'=@6'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 64 = 64  
begin  
  select @stmt = @stmt + @spacer + N'[state]' + N'=@7'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 128 = 128  
begin  
  select @stmt = @stmt + @spacer + N'[zip]' + N'=@8'  
  select @spacer = N','  
end  
if substring(@bitmap,2,1) & 1 = 1  
begin  
  select @stmt = @stmt + @spacer + N'[contract]' + N'=@9'  
  select @spacer = N','  
end  
select @stmt = @stmt + N' where [au_id] = @1'  
exec sp_executesql @stmt, N' @1 varchar(11),@2 varchar(40),@3 varchar(20),@4 char(12),@5 varchar(40),  
                             @6 varchar(20),@7 char(2),@8 char(5),@9 bit',@pkc1,@c2,@c3,@c4,@c5,@c6,@c7,@c8,@c9  
  
if @@rowcount = 0  
   if @@microsoftversion>0x07320000  
      exec sp_MSreplraiserror 20598  
```  
  
 Depois de executar esse procedimento armazenado, você pode usar o script resultante para criar o procedimento armazenado manualmente nos Assinantes.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
