---
title: DM db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 028c3a2fe26d448373fcb9c4a00d2916a1bb34e5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726754"
---
# <a name="spatial-data---sysdmdbobjectsdisabledoncompatibilitylevelchange"></a>Dados espaciais - DM db_objects_disabled_on_compatibility_level_change
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
|**class**|**int**|1 = restrições<br /><br /> 7 = índices e heaps|  
|**class_desc**|**nvarchar(60)**|OBJECT ou COLUMN para restrições<br /><br /> INDEX para índices e heaps|  
|**major_id**|**int**|OBJECT ID de restrições<br /><br /> OBJECT ID da tabela que contém índices e heaps|  
|**minor_id**|**int**|NULL para restrições<br /><br /> Index_id para índices e heaps|  
|**dependência**|**nvarchar(60)**|Descrição da dependência que está causando a desabilitação da restrição ou do índice. Os mesmos valores também são usados nos avisos que são lançados durante atualização. Os exemplos incluem o seguinte:<br /><br /> "space" para um intrínseco<br /><br /> "geometry" para um sistema UDT<br /><br /> "geography::Parse" para um método de um sistema UDT|  
  
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
  
-   **Geography:: Parse**  
  
-   **Geography:: reduzir**  
  
### <a name="behavior-of-the-disabled-objects"></a>Comportamento dos objetos desabilitados  
 **Índices**  
  
 Se o índice clusterizado está desabilitado ou se um índice não agrupado for forçado, o seguinte erro será gerado: "o processador de consultas não consegue produzir um plano porque o índice ' %. \*ls' na tabela ou exibição ' %. \*ls' está desabilitado. " Para habilitar novamente esses objetos, reconstrua os índices após a atualização chamando **ALTER INDEX ON... RECOMPILAR**.  
  
 **Heaps**  
  
 Se uma tabela com um heap desabilitado for usada, o erro a seguir será lançado. Para habilitar novamente esses objetos, reconstrua após a atualização chamando **ALTER INDEX ON todos... RECOMPILAR**.  
  
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
  
 **Restrições de verificação e as chaves estrangeiras**  
  
 Restrições de verificação desabilitadas e chave estrangeiras não lançam um erro. Porém, as restrições não são impostas quando linhas são modificadas. Para habilitar novamente esses objetos, as restrições de verificação depois de atualizar chamando **ALTER TABLE... RESTRIÇÃO de verificação**.  
  
 **Colunas computadas persistentes**  
  
 Como não é possível desabilitar uma única coluna, a tabela inteira é desabilitada com a desabilitação do índice clusterizado ou heap.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DATABASE STATE.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma consulta em **DM db_objects_disabled_on_compatibility_level_change** para localizar os objetos afetados, alterando o nível de compatibilidade para 120.  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
