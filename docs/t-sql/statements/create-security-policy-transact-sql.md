---
title: "Criar política de segurança (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SECURITY_POLICY_TSQL
- CREATE SECURITY
- SECURITY
- CREATE_SECURITY_POLICY_TSQL
- CREATE_SECURITY_TSQL
- SECURITY POLICY
- SECURITY_TSQL
- CREATE SECURITY POLICY
dev_langs:
- TSQL
helpviewer_keywords:
- RLS
- CREATE SECURITY POLICY statement
- Row-Level Security
ms.assetid: d6ab70ee-0fa2-469c-96f6-a3c16d673bc8
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53292dc3f9f5cbd36913276496084d4648f13520
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-security-policy-transact-sql"></a>Criar política de segurança (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Cria uma política de segurança para segurança em nível de linha.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | arguments } [ , …n] ) ON table_schema_name. table_name    
      [ <block_dml_operation> ] , [ , …n] 
    [ WITH ( STATE = { ON | OFF }  [,] [ SCHEMABINDING = { ON | OFF } ] ) ]  
    [ NOT FOR REPLICATION ] 
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *security_policy_name*  
 O nome da política de segurança. Nomes de políticas de segurança devem obedecer às regras de identificadores e devem ser exclusivos dentro do banco de dados e em seu esquema.  
  
 *schema_name*  
 É o nome do esquema ao qual a política de segurança pertence. *schema_name* é necessária devido a associação de esquema.  
  
 [FILTRO | BLOCO]  
 O tipo de predicado de segurança para a função que está sendo associada à tabela de destino. Os predicados de filtro filtram silenciosamente as linhas que estão disponíveis para operações de leitura. Predicados de bloco explicitamente as operações de gravação de blocos que violam a função de predicado.  
  
 *tvf_schema_name.security_predicate_function_name*  
 É a função de valor de tabela embutida que será usada como um predicado e que serão aplicadas em consultas em uma tabela de destino. No máximo um predicado de segurança pode ser definido para uma determinada operação DML em uma tabela específica. A função de valor de tabela embutida deve ter sido criada usando a opção SCHEMABINDING.  
  
 { *column_name* | *argumentos* }  
 O nome da coluna ou expressão usada como parâmetros para a função de predicado de segurança. As colunas na tabela de destino podem ser usadas como argumentos para a função de predicado. Expressões que incluem literais, internos e expressões que usam operadores aritméticos podem ser usadas.  
  
 *table_schema_name.table_name*  
 É a tabela de destino a qual o predicado de segurança será aplicado. Várias políticas de segurança desabilitadas podem direcionar uma única tabela para uma determinada operação DML, mas apenas uma pode ser habilitada em um determinado momento.  
  
 *\<block_dml_operation >* a operação DML específica para o qual o predicado de bloco será aplicado. Depois, especifica que o predicado será avaliado nos valores das linhas após a operação DML foi executada (INSERT ou UPDATE). ANTES, especifica que o predicado será avaliado nos valores das linhas antes que a operação DML seja executada (UPDATE ou DELETE). Se nenhuma operação for especificada, o predicado será aplicada a todas as operações.  
  
 [ESTADO = {ON | **OFF** }]  
 Habilita ou desabilita a política de segurança ao impor seus predicados de segurança nas tabelas de destino. Se não especificado, a política de segurança que está sendo criada é habilitada.  
  
 [SCHEMABINDING = {ON | OFF}]  
 Indica se todas as funções de predicado na política devem ser criadas com a opção SCHEMABINDING. Por padrão, todas as funções devem ser criadas com SCHEMABINDING.  
  
 NOT FOR REPLICATION  
 Indica que a política de segurança não deve ser executada quando um agente de replicação modifica o objeto de destino. Para obter mais informações, consulte [Controlar o comportamento de gatilhos e restrições durante a sincronização &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
 [*table_schema_name*.] *table_name*  
 É a tabela de destino a qual o predicado de segurança será aplicado. Várias políticas de segurança desabilitadas podem direcionar uma única tabela, mas apenas uma pode ser habilitada em um determinado momento.  
  
## <a name="remarks"></a>Comentários  
 Ao usar funções de predicado com tabelas com otimização de memória, você deve incluir **SCHEMABINDING** e usar o **WITH NATIVE_COMPILATION** dica de compilação.  
  
 Os predicados de bloqueio são avaliados depois que a operação DML correspondente é executada. Portanto, uma consulta READ UNCOMMITTED pode ver valores transitórios que serão revertidos.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY SECURITY POLICY e a permissão ALTER no esquema.  
  
 Além disso, as seguintes permissões são necessárias para cada predicado que é adicionado:  
  
-   Permissões SELECT e REFERENCES na função que está sendo usada como um predicado.  
  
-   Permissão REFERENCES na tabela de destino que está sendo associada à política.  
  
-   Permissão REFERENCES em todas as colunas da tabela de destino usada como argumentos.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o uso da sintaxe **CREATE SECURITY POLICY** . Para obter um exemplo de um cenário de política de segurança completa, consulte [segurança em nível de linha](../../relational-databases/security/row-level-security.md).  
  
### <a name="a-creating-a-security-policy"></a>A. Criação de uma política de segurança  
 A sintaxe a seguir cria uma política de segurança com um predicado de filtro para a tabela Customer e deixa a política de segurança desabilitada.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate]([CustomerId])   
ON [dbo].[Customer];  
```  
  
### <a name="b-creating-a-policy-that-affects-multiple-tables"></a>B. Criação de uma política que afeta várias tabelas  
 A sintaxe a seguir cria uma política de segurança com três predicados de filtro em três tabelas diferentes e habilita a política de segurança.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([CustomerId])   
    ON [dbo].[Customer],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([VendorId])   
    ON [dbo].[ Vendor],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate2]([WingId])   
    ON [dbo].[Patient]  
WITH (STATE = ON);  
```  
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>C. Criando uma política com vários tipos de predicados de segurança  
 Adicionando um predicado de filtro e um predicado de bloco para a tabela de vendas.  
  
```  
CREATE SECURITY POLICY rls.SecPol  
    ADD FILTER PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales,  
    ADD BLOCK PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança em nível de linha](../../relational-databases/security/row-level-security.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys. security_predicates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  


