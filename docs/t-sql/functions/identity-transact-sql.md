---
title: '@@IDENTITY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d5a41eec147978e3e794c77e4c79336daa780e29
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113436"
---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40;IDENTITY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  É uma função de sistema que retorna o último valor de identidade inserido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@IDENTITY  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **numeric(38,0)**  
  
## <a name="remarks"></a>Comentários  
 Após a conclusão de uma instrução INSERT, SELECT INTO ou de cópia em massa, @@IDENTITY conterá o último valor de identidade gerado pela instrução. Se a instrução não afetou nenhuma tabela com colunas de identidade, @@IDENTITY retorna NULL. Se várias linhas forem inseridas, gerando vários valores de identidade, @@IDENTITY retornará o último valor de identidade gerado. Se a instrução disparar um ou mais gatilhos que executam inserções que geram valores de identidade, a chamada a @@IDENTITY imediatamente após a instrução retornará o último valor de identidade gerado pelos gatilhos. Se um gatilho for disparado após uma ação de inserção em uma tabela que contém uma coluna de identidade e fizer uma inserção em outra tabela que não contém uma coluna de identidade, @@IDENTITY retornará o valor de identidade da primeira inserção. O valor de @@IDENTITY não será revertido para uma configuração anterior se a instrução INSERT ou SELECT INTO ou a cópia em massa falhar, ou se a transação for revertida.  
  
 Instruções e transações com falha podem alterar a identidade atual de uma tabela e criar lacunas nos valores da coluna de identidade. O valor de identidade nunca é revertido, mesmo que a transação que tentou inserir o valor na tabela não seja confirmada. Por exemplo, se uma instrução INSERT falhar por causa de uma violação IGNORE_DUP_KEY, o valor de identidade atual para a tabela ainda será incrementado.  
  
 @@IDENTITY, SCOPE_IDENTITY e IDENT_CURRENT são funções semelhantes porque retornam o último valor inserido na coluna IDENTITY de uma tabela.  
  
 @@IDENTITY e SCOPE_IDENTITY retornam o último valor de identidade gerado em qualquer tabela na sessão atual. Entretanto, SCOPE_IDENTITY retorna o valor apenas dentro do escopo atual; @@IDENTITY não está limitado a um escopo específico.  
  
 IDENT_CURRENT não é limitado por escopo e sessão, mas a uma tabela especificada. IDENT_CURRENT retorna o valor de identidade gerado para uma tabela específica em qualquer sessão e escopo. Para obter mais informações, consulte [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md).  
  
 O escopo da função @@IDENTITY é a sessão atual no servidor local no qual ela é executada. Essa função não pode ser se aplicada a servidores remotos ou vinculados. Para obter um valor de identidade em um servidor diferente, execute um procedimento armazenado no servidor remoto ou vinculado e faça com que esse procedimento (ao ser executado no contexto do servidor remoto ou vinculado) obtenha o valor de identidade e o retorne para a conexão de chamada no servidor local.  
  
 A replicação pode afetar o valor de @@IDENTITY, já que ele é usado dentro dos gatilhos de replicação e procedimentos armazenados. @@IDENTITY não é um indicador confiável da identidade mais recente criada pelo usuário se a coluna faz parte de um artigo de replicação. Use a sintaxe da função SCOPE_IDENTITY() em vez de @@IDENTITY. Para obter mais informações, consulte [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  O procedimento armazenado de chamada ou a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] deve ser reescrito para usar a função `SCOPE_IDENTITY()`, que retorna a última identidade usada dentro do escopo dessa instrução de usuário, e não a identidade dentro do escopo do gatilho aninhado usado pela replicação.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir insere uma linha em uma tabela com uma coluna de identidade (`LocationID`) e usa `@@IDENTITY` para exibir o valor de identidade usado na nova linha.  
  
```  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
