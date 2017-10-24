---
title: '@@IDENTITY (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88cdaa1362e5d60b0f880c66c7fb7038ddb9f126
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40identity-transact-sql"></a>& #x 40; & #x 40; identidade (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  É uma função de sistema que retorna o último valor de identidade inserido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Comentários  
 Após um INSERT, SELECT INTO ou em massa a instrução de cópia for concluída, @@IDENTITY contém o último valor de identidade gerado pela instrução. Se a instrução não afetou todas as tabelas com colunas de identidade, @@IDENTITY retorna NULL. Se várias linhas forem inseridas, gerando vários valores de identidade, @@IDENTITY retorna o último valor de identidade gerado. Se a instrução acionar um ou mais disparadores que executem inserções que geram valores de identidade, chamando@IDENTITY imediatamente após a instrução retorna o último valor de identidade gerado pelos disparadores. Se um disparador é acionado depois de uma ação de inserção em uma tabela que tem uma coluna de identidade e o gatilho insere em outra tabela que não tem uma coluna de identidade, @@IDENTITY retorna o valor de identidade da primeira inserção. O @@IDENTITY não será revertido para uma configuração anterior se a cópia de instrução ou bulk INSERT ou SELECT INTO falhar ou se a transação for revertida.  
  
 Instruções e transações com falha podem alterar a identidade atual de uma tabela e criar lacunas nos valores da coluna de identidade. O valor de identidade nunca é revertido, mesmo que a transação que tentou inserir o valor na tabela não seja confirmada. Por exemplo, se uma instrução INSERT falhar por causa de uma violação IGNORE_DUP_KEY, o valor de identidade atual para a tabela ainda será incrementado.  
  
 @@IDENTITY, SCOPE_IDENTITY e IDENT_CURRENT são funções semelhantes porque retornam o último valor inserido na coluna de identidade de uma tabela.  
  
 @@IDENTITY e SCOPE_IDENTITY retornam o último valor de identidade gerado em qualquer tabela na sessão atual. Entretanto, SCOPE_IDENTITY retorna o valor somente dentro do escopo atual; @@IDENTITY não está limitado a um escopo específico.  
  
 IDENT_CURRENT não é limitado por escopo e sessão, mas a uma tabela especificada. IDENT_CURRENT retorna o valor de identidade gerado para uma tabela específica em qualquer sessão e escopo. Para obter mais informações, consulte [IDENT_CURRENT &#40; Transact-SQL &#41; ](../../t-sql/functions/ident-current-transact-sql.md).  
  
 O escopo do @@IDENTITY função é a sessão atual no servidor local no qual ele é executado. Essa função não pode ser se aplicada a servidores remotos ou vinculados. Para obter um valor de identidade em um servidor diferente, execute um procedimento armazenado no servidor remoto ou vinculado e faça com que esse procedimento (ao ser executado no contexto do servidor remoto ou vinculado) obtenha o valor de identidade e o retorne para a conexão de chamada no servidor local.  
  
 A replicação pode afetar o @@IDENTITY valor, pois ele é usado dentro de procedimentos armazenados e gatilhos de replicação. @@IDENTITY não é um indicador confiável da identidade de usuário criado mais recente se a coluna faz parte de um artigo de replicação. Você pode usar a sintaxe da função SCOPE_IDENTITY () em vez de @@IDENTITY. Para obter mais informações, consulte [SCOPE_IDENTITY &#40; Transact-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  A chamar um procedimento armazenado ou [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução deve ser reescrita para usar o `SCOPE_IDENTITY()` função, que retorna a última identidade usada dentro do escopo daquela instrução de usuário e não a identidade dentro do escopo do disparador aninhado, usado por replicação.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40; Transact-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

