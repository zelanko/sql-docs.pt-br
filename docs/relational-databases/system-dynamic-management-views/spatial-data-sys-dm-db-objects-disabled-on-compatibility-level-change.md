---
title: sys.DM db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a62064e86154d626b2ade08b4f52cc617bb4f29c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spatial-data---sysdmdbobjectsdisabledoncompatibilitylevelchange"></a>Dados espaciais - sys.DM db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Lista os índices e as restrições que serão desabilitados como resultado da alteração do nível de compatibilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Índices e restrições que contêm colunas computadas persistentes cujas expressões usam UDTs espaciais serão desabilitadas depois de atualizar ou alterar nível de compatibilidade. Use essa função de gerenciamento dinâmico para determinar o impacto de uma alteração no nível de compatibilidade.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="Arguments"></a> Argumentos  
 *compatibility_level*  
 **int** que identifica o nível de compatibilidade que você planeja definir.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**class**|**Int**|1 = restrições<br /><br /> 7 = índices e heaps|  
|**class_desc**|**nvarchar(60)**|OBJECT ou COLUMN para restrições<br /><br /> INDEX para índices e heaps|  
|**major_id**|**Int**|OBJECT ID de restrições<br /><br /> OBJECT ID da tabela que contém índices e heaps|  
|**minor_id**|**Int**|NULL para restrições<br /><br /> Index_id para índices e heaps|  
|**Dependência**|**nvarchar(60)**|Descrição da dependência que está causando a desabilitação da restrição ou do índice. Os mesmos valores também são usados nos avisos que são lançados durante atualização. Os exemplos incluem o seguinte:<br /><br /> "space" para um intrínseco<br /><br /> "geometry" para um sistema UDT<br /><br /> "geography::Parse" para um método de um sistema UDT|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Colunas computadas persistentes que usam algumas funções intrínsecas são desabilitadas quando o nível de compatibilidade é alterado. Além disso, colunas computadas persistentes que usam qualquer método de geometria ou geografia são desabilitadas quando um banco de dados é atualizado.  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>Que funções causam a desabilitação de colunas computadas persistentes?  
 Quando as funções a seguir são usadas na expressão de uma coluna computada persistente, elas causam a desabilitação de índices e restrições que fazem referência a essas colunas quando o nível de compatibilidade é alterado de 80 para 90:  
  
-   **IsNumeric**  
  
 Quando as funções a seguir são usadas na expressão de uma coluna computada persistente, elas causam a desabilitação de índices e restrições que fazem referência a essas colunas quando o nível de compatibilidade é alterado de 100 para 110 ou superior:  
  
-   **Soundex**  
  
-   **Geography:: GeomFromGML**  
  
-   **Geography:: STGeomFromText**  
  
-   **Geography:: STLineFromText**  
  
-   **Geography:: STPolyFromText**  
  
-   **Geography:: STMPointFromText**  
  
-   **Geography:: STMLineFromText**  
  
-   **Geography:: STMPolyFromText**  
  
-   **Geography:: STGeomCollFromText**  
  
-   **Geography:: STGeomFromWKB**  
  
-   **Geography:: STLineFromWKB**  
  
-   **Geography:: STPolyFromWKB**  
  
-   **Geography:: STMPointFromWKB**  
  
-   **Geography:: STMLineFromWKB**  
  
-   **Geography:: STMPolyFromWKB**  
  
-   **Geography:: STUnion**  
  
-   **Geography:: STIntersection**  
  
-   **Geography:: STDifference**  
  
-   **Geography:: STSymDifference**  
  
-   **Geography:: STBuffer**  
  
-   **Geography:: BufferWithTolerance**  
  
-   **Geography:: analisar**  
  
-   **Geography:: reduzir**  
  
### <a name="behavior-of-the-disabled-objects"></a>Comportamento dos objetos desabilitados  
 **Índices**  
  
 Se o índice clusterizado está desabilitado ou se um índice não clusterizado for forçado, acontece o seguinte erro: "o processador de consultas é não consegue produzir um plano porque o índice ' %. \*ls' na tabela ou exibição ' %. \*ls' está desabilitado. " Para habilitar novamente esses objetos, reconstrua os índices após a atualização chamando **ALTER INDEX ON... RECRIAR**.  
  
 **Heaps**  
  
 Se uma tabela com um heap desabilitado for usada, o erro a seguir será lançado. Para habilitar novamente esses objetos, reconstrua após a atualização chamando **ALTER INDEX ON todos... RECRIAR**.  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 Se você tentar reconstruir o heap durante uma operação online, um erro será gerado.  
  
 **Restrições de verificação e chaves estrangeiras**  
  
 Restrições de verificação desabilitadas e chave estrangeiras não lançam um erro. Porém, as restrições não são impostas quando linhas são modificadas. Para habilitar novamente esses objetos, as restrições de verificação depois de atualizar chamando **ALTER TABLE... RESTRIÇÃO de verificação**.  
  
 **Colunas computadas persistentes**  
  
 Como não é possível desabilitar uma única coluna, a tabela inteira é desabilitada com a desabilitação do índice clusterizado ou heap.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DATABASE STATE.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma consulta em **sys.DM db_objects_disabled_on_compatibility_level_change** para localizar os objetos afetados, alterando o nível de compatibilidade para 120.  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
