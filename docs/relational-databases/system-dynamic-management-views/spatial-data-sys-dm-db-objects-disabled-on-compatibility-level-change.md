---
title: sys. dm_db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 300b988ce74a22dad3384920bb93fd45191128e8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832610"
---
# <a name="spatial-data---sysdm_db_objects_disabled_on_compatibility_level_change"></a>Dados espaciais-sys. dm_db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Lista os índices e as restrições que serão desabilitados como resultado da alteração do nível de compatibilidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Índices e restrições que contêm colunas computadas persistentes cujas expressões usam UDTs espaciais serão desabilitadas depois de atualizar ou alterar nível de compatibilidade. Use essa função de gerenciamento dinâmico para determinar o impacto de uma alteração no nível de compatibilidade.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 *compatibility_level*  
 **int** que identifica o nível de compatibilidade que você planeja definir.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**classes**|**int**|1 = restrições<br /><br /> 7 = índices e heaps|  
|**class_desc**|**nvarchar(60)**|OBJECT ou COLUMN para restrições<br /><br /> INDEX para índices e heaps|  
|**major_id**|**int**|OBJECT ID de restrições<br /><br /> OBJECT ID da tabela que contém índices e heaps|  
|**minor_id**|**int**|NULL para restrições<br /><br /> Index_id para índices e heaps|  
|**Estados**|**nvarchar(60)**|Descrição da dependência que está causando a desabilitação da restrição ou do índice. Os mesmos valores também são usados nos avisos que são lançados durante atualização. Os exemplos incluem o seguinte:<br /><br /> "space" para um intrínseco<br /><br /> "geometry" para um sistema UDT<br /><br /> "geography::Parse" para um método de um sistema UDT|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Colunas computadas persistentes que usam algumas funções intrínsecas são desabilitadas quando o nível de compatibilidade é alterado. Além disso, colunas computadas persistentes que usam qualquer método de geometria ou geografia são desabilitadas quando um banco de dados é atualizado.  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>Que funções causam a desabilitação de colunas computadas persistentes?  
 Quando as funções a seguir são usadas na expressão de uma coluna computada persistente, elas causam a desabilitação de índices e restrições que fazem referência a essas colunas quando o nível de compatibilidade é alterado de 80 para 90:  
  
-   **IsNumeric**  
  
 Quando as funções a seguir são usadas na expressão de uma coluna computada persistente, elas causam a desabilitação de índices e restrições que fazem referência a essas colunas quando o nível de compatibilidade é alterado de 100 para 110 ou superior:  
  
-   **SOUNDEX**  
  
-   **Geography:: GeomFromGML**  
  
-   **Geography:: STGeomFromText**  
  
-   **Geografia:: STLineFromText**  
  
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
  
-   **Geografia:: Parse**  
  
-   **Geography:: Reduce**  
  
### <a name="behavior-of-the-disabled-objects"></a>Comportamento dos objetos desabilitados  
 **Índices**  
  
 Se o índice clusterizado estiver desabilitado ou se um índice não clusterizado for forçado, o seguinte erro será gerado: "o processador de consultas não pode produzir um plano porque o índice '%. \* ls "na tabela ou exibição"%. \* ls "está desabilitado". Para reabilitar esses objetos, recompile os índices após a atualização chamando **ALTER INDEX on... Recompilar**.  
  
 **Heaps**  
  
 Se uma tabela com um heap desabilitado for usada, o erro a seguir será lançado. Para reabilitar esses objetos, recompile após a atualização chamando **ALTER INDEX All on... Recompilar**.  
  
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
  
 Se você tentar recriar o heap durante uma operação online, um erro será gerado.  
  
 **Verificar restrições e chaves estrangeiras**  
  
 Restrições de verificação desabilitadas e chave estrangeiras não lançam um erro. Porém, as restrições não são impostas quando linhas são modificadas. Para reabilitar esses objetos, verifique as restrições após a atualização chamando **ALTER TABLE... RESTRIÇÃO de verificação**.  
  
 **Colunas computadas persistentes**  
  
 Como não é possível desabilitar uma única coluna, a tabela inteira é desabilitada com a desabilitação do índice clusterizado ou heap.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige a permissão VIEW DATABASE STATE.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma consulta em **Sys. dm_db_objects_disabled_on_compatibility_level_change** para localizar os objetos afetados alterando o nível de compatibilidade para 120.  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
