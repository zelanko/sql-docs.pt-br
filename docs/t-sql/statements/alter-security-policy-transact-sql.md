---
title: ALTER SECURITY POLICY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2943e1c1d85e1868ba51433a213e0c6ebfafcdd3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33070363"
---
# <a name="alter-security-policy-transact-sql"></a>ALTER SECURITY POLICY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Altera uma política de segurança.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 security_policy_name  
 O nome da política de segurança. Nomes de políticas de segurança devem obedecer às regras de identificadores e devem ser exclusivos dentro do banco de dados e em seu esquema.  
  
 schema_name  
 É o nome do esquema ao qual a política de segurança pertence. *schema_name* é obrigatório devido à associação de esquema.  
  
 [ FILTER | BLOCK ]  
 O tipo de predicado de segurança para a função que está sendo associada à tabela de destino. Os predicados FILTER filtram silenciosamente as linhas que estão disponíveis para operações de leitura. Os predicados BLOCK bloqueiam explicitamente as operações de gravação que violam a função de predicado.  
  
 tvf_schema_name.security_predicate_function_name  
 É a função de valor de tabela embutida que será usada como um predicado e que serão aplicadas em consultas em uma tabela de destino. No máximo um predicado de segurança pode ser definido para uma determinada operação DML em uma tabela específica. A função de valor de tabela embutida deve ter sido criada usando a opção SCHEMABINDING.  
  
 { column_name | arguments }  
 O nome da coluna ou expressão usada como parâmetros para a função de predicado de segurança. As colunas na tabela de destino podem ser usadas como argumentos para a função de predicado. Expressões que incluem literais, internos e expressões que usam operadores aritméticos podem ser usadas.  
  
 *table_schema_name.table_name*  
 É a tabela de destino a qual o predicado de segurança será aplicado. Várias políticas de segurança desabilitadas podem ser direcionadas a uma operação DML específica, mas apenas uma pode ser habilitada em determinado momento.  
  
 *\<block_dml_operation>*  
 A operação DML específica para à qual o predicado de bloqueio será aplicado. AFTER especifica que o predicado será avaliado nos valores das linhas após a execução da operação DML (INSERT ou UPDATE). BEFORE especifica que o predicado será avaliado nos valores das linhas antes que a operação DML seja executada (UPDATE ou DELETE). Se nenhuma operação for especificada, o predicado será aplicado a todas as operações.  
  
 Você não pode usar ALTER para alterar a operação para a qual um predicado de bloqueio será aplicado, porque a operação é usada para identificar exclusivamente o predicado. Em vez disso, deve remover o predicado e adicionar um novo para a nova operação.  
  
 WITH ( STATE = { ON | OFF } )  
 Habilita ou desabilita a política de segurança ao impor seus predicados de segurança nas tabelas de destino. Se não especificado, a política de segurança que está sendo criada é desabilitada.  
  
 NOT FOR REPLICATION  
 Indica que a política de segurança não deve ser executada quando um agente de replicação modifica o objeto de destino. Para obter mais informações, consulte [Controlar o comportamento de gatilhos e restrições durante a sincronização &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
 table_schema_name.table_name  
 É a tabela de destino a qual o predicado de segurança será aplicado. Várias políticas de segurança desabilitadas podem direcionar uma única tabela, mas apenas uma pode ser habilitada em um determinado momento.  
  
## <a name="remarks"></a>Remarks  
 A instrução ALTER SECURITY POLICY está no escopo de uma transação. Se a transação for revertida, a instrução também será revertida.  
  
 Ao usar funções de predicado com tabelas com otimização de memória, as políticas de segurança devem incluir **SCHEMABINDING** e usar a dica de compilação **WITH NATIVE_COMPILATION**. O argumento SCHEMABINDING não podem ser alterados com a instrução ALTER porque ela se aplica a todos os predicados. Para alterar a associação de esquema, você deve remover e recriar a política de segurança.  
  
 Os predicados de bloqueio são avaliados depois que a operação DML correspondente é executada. Portanto, uma consulta READ UNCOMMITTED pode exibir valores transitórios que serão revertidos.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY SECURITY POLICY.  
  
 Além disso, as seguintes permissões são necessárias para cada predicado que é adicionado:  
  
-   Permissões SELECT e REFERENCES na função que está sendo usada como um predicado.  
-   Permissão REFERENCES na tabela de destino que está sendo associada à política.  
-   Permissão REFERENCES em todas as colunas da tabela de destino usada como argumentos.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o uso da sintaxe **ALTER SECURITY POLICY** . Para obter um exemplo de um cenário de política de segurança completo, consulte [Segurança em nível de linha](../../relational-databases/security/row-level-security.md).  
  
### <a name="a-adding-an-additional-predicate-to-a-policy"></a>A. Adicionando um predicado extra a uma política  
 A sintaxe a seguir altera uma política de segurança, adicionando um predicado de filtro na tabela `mytable`.  
  
```  
ALTER SECURITY POLICY pol1   
    ADD FILTER PREDICATE schema_preds.SecPredicate(column1)   
    ON myschema.mytable;  
```  
  
### <a name="b-enabling-an-existing-policy"></a>B. Habilitando uma política existente  
 O exemplo a seguir usa a sintaxe ALTER para habilitar uma política de segurança.  
  
```  
ALTER SECURITY POLICY pol1 WITH ( STATE = ON );  
```  
  
### <a name="c-adding-and-dropping-multiple-predicates"></a>C. Adicionando e removendo vários predicados  
 A sintaxe a seguir altera uma política de segurança, adicionando predicados de filtro nas tabelas `mytable1` e `mytable3` e removendo o predicado de filtro na tabela `mytable2`.  
  
```  
ALTER SECURITY POLICY pol1  
ADD FILTER PREDICATE schema_preds.SecPredicate1(column1)   
    ON myschema.mytable1,  
DROP FILTER PREDICATE   
    ON myschema.mytable2,  
ADD FILTER PREDICATE schema_preds.SecPredicate2(column2, 1)   
    ON myschema.mytable3;  
```  
  
### <a name="d-changing-the-predicate-on-a-table"></a>D. Alterando o predicado em uma tabela  
 A sintaxe a seguir altera o predicado do filtro existente na tabela mytable para a função SecPredicate2.  
  
```  
ALTER SECURITY POLICY pol1  
    ALTER FILTER PREDICATE schema_preds.SecPredicate2(column1)  
        ON myschema.mytable;  
```  
  
### <a name="e-changing-a-block-predicate"></a>E. Alterando um predicado de bloqueio  
 Alterar a função de predicado de bloqueio para uma operação em uma tabela.  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
