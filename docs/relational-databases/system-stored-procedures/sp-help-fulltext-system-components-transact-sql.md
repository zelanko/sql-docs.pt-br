---
description: sp_help_fulltext_system_components (Transact-SQL)
title: sp_help_fulltext_system_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_components_TSQL
- sp_help_fulltext_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_system_components
ms.assetid: ac1fc7a0-7f46-4a12-8c5c-8d378226a8ce
author: CarlRabeler
ms.author: carlrab
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0686017e612b5d9d7d2c1f932321a965b7f1448a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493198"
---
# <a name="sp_help_fulltext_system_components-transact-sql"></a>sp_help_fulltext_system_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Retorna informações para os separadores de palavras, filtro e manipuladores de protocolos. **sp_help_fulltext_system_components** também retorna uma lista de identificadores de bancos de dados e catálogos de texto completo que usaram o componente especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_system_components   
         { 'all'| [ @component_type = ] 'component_type' }  
    , [ @param = ] 'param'  
```  
  
## <a name="arguments"></a>Argumentos  
 'all'  
 Retorna informações de todos os componentes de texto completo.  
  
`[ @component_type = ] component_type` Especifica o tipo de componente. *component_type* pode ser um dos seguintes:  
  
-   **separador**  
  
-   **sem**  
  
-   **manipulador de protocolo**  
  
-   **FullPath**  
  
 Se um caminho completo for especificado, *param* também deverá ser especificado com o caminho completo para a DLL do componente, ou uma mensagem de erro será retornada.  
  
`[ @param = ] param` Dependendo do tipo de componente, este é um dos seguintes: um LCID (identificador de localidade), a extensão de arquivo com o prefixo ".", o nome completo do componente do manipulador de protocolo ou o caminho completo para a DLL do componente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou (1) falha  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O conjunto de resultados a seguir é retornado para os componentes de sistema.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**componenttype**|**sysname**|Tipo de componente. Um dos seguintes:<br /><br /> filtro<br /><br /> protocol handler<br /><br /> wordbreaker|  
|**ComponentName**|**sysname**|Nome do componente.|  
|**clsid**|**uniqueidentifier**|Identificador de classe do componente.|  
|**FullPath**|**nvarchar(256)**|Caminho até a localização do componente.<br /><br /> NULL = o chamador não é um membro da função de servidor fixa **ServerAdmin** .|  
|**version**|**nvarchar(30)**|A versão do componente.|  
|**fabricante**|**sysname**|Nome do fabricante do componente.|  
  
 O conjunto de resultados a seguir será retornado somente se existir um ou mais de um catálogo de texto completo que use *component_type*.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DBID**|**int**|ID do banco de dados.|  
|**ftcatid**|**int**|Identificação do catálogo de texto completo.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função **pública** ; no entanto, os usuários só podem ver informações sobre os catálogos de texto completo para os quais têm permissão VIEW DEFINITION. Somente os membros da função fixa **serveradmin** podem ver os valores na coluna **fullpath** .  
  
## <a name="remarks"></a>Comentários  
 Este método é importante na preparação para uma atualização. Execute o procedimento armazenado em um determinado banco de dados e use a saída para determinar se um catálogo específico será afetado pela atualização.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-full-text-system-components"></a>a. Listando todos os componentes de texto completo do sistema  
 O exemplo a seguir lista todos os componentes de texto completo do sistema que tenham sido registrados na instância de servidor.  
  
```  
EXEC sp_help_fulltext_system_components 'all';  
GO  
```  
  
### <a name="b-listing-word-breakers"></a>B. Listando separadores de palavras  
 O exemplo a seguir lista todos os separadores de palavras registrados na instância do serviço.  
  
```  
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```  
  
### <a name="c-determining-whether-a-specific-word-breaker-is-registered"></a>C. Determinando se um separador de palavras específico está registrado  
 O exemplo a seguir listará o separador de palavras do idioma turco (LCID = 1055) se este tiver sido instalado no sistema e registrado na instância do serviço. Este exemplo especifica os nomes de parâmetro, ** \@ component_type** e ** \@ param**.  
  
```  
EXEC sp_help_fulltext_system_components @component_type = 'wordbreaker', @param = 1055;  
GO  
```  
  
 Por padrão, esse separador de palavras não é instalado, portanto, o conjunto de resultados é vazio.  
  
### <a name="d-determining-whether-a-specific-filter-has-been-registered"></a>D. Determinando se um filtro específico foi registrado  
 O exemplo a seguir listará o filtro do componente .xdoc se ele tiver sido instalado manualmente no sistema e registrado na instância do servidor.  
  
```  
EXEC sp_help_fulltext_system_components 'filter', '.xdoc';  
GO  
```  
  
 Por padrão, esse filtro não é instalado, portanto, o conjunto de resultados é vazio.  
  
### <a name="e-listing-a-specific-dll-file"></a>E. Listando um arquivo .dll específico  
 O exemplo a seguir lista um arquivo .ddl específico, `nlhtml.dll`, o qual é instalado por padrão.  
  
```  
EXEC sp_help_fulltext_system_components 'fullpath',   
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\nlhtml.dll';  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir ou alterar filtros registrados e separadores de palavras](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)   
 [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Os procedimentos armazenados de pesquisa de texto completo e de semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
