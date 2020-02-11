---
title: sys. syslanguages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syslanguages
- sys.syslanguages_TSQL
- syslanguages
- syslanguages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syslanguages system table
- sys.syslanguages compatibility view
ms.assetid: f216d1cd-997c-42f0-a737-abbdfcd88383
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc152b8241b775f9fd686f8a31363cb4fca39de4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70874873"
---
# <a name="syssyslanguages-transact-sql"></a>sys.syslanguages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada idioma presente na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|langid|**smallint**|ID exclusiva de idioma.|  
|dateformat|**nchar(3)**|Ordem de data, por exemplo, DMA.|  
|datefirst|**tinyint**|Primeiro dia da semana: 1 para segunda-feira, 2 para terça-feira e assim por diante, até 7 para domingo.|  
|atualizar|**int**|Reservado para uso do sistema.|  
|name|**sysname**|Nome oficial do idioma, por exemplo, francês.|  
|alias|**sysname**|Nome de idioma alternativo, por exemplo, francês.|  
|months|**nvarchar (372)**|Lista de nomes de meses completos separados por vírgula, de janeiro a dezembro, com cada nome contendo até 20 caracteres.|  
|shortmonths|**nvarchar (132)**|Lista de nomes de meses abreviados separados por vírgula, de janeiro a dezembro, com cada nome contendo até 9 caracteres.|  
|dias|**nvarchar (217)**|Lista de nomes de dias separados por vírgula, de segunda-feira a domingo, com cada nome contendo até 30 caracteres.|  
|lcid|**int**|ID de localidade do [!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows para o idioma.|  
|msglangid|**smallint**|ID do grupo de mensagens do [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] contém os seguintes idiomas instalados.  
  
|Nome em inglês|LCID do Windows|[!INCLUDE[ssDE](../../includes/ssde-md.md)]ID do grupo de mensagens|  
|---------------------|------------------|-----------------------------------------|  
|Inglês|1033|1033|  
|Alemão|1031|1031|  
|Francês|1036|1036|  
|Japonês|1041|1041|  
|Dinamarquês|1030|1030|  
|Espanhol|3082|3082|  
|Italiano|1040|1040|  
|Holandês|1043|1043|  
|Norueguês|2068|2068|  
|Português|2070|2070|  
|Finlandês|1035|1035|  
|Sueco|1053|1053|  
|Tcheco|1029|1029|  
|Húngaro|1038|1038|  
|Polonês|1045|1045|  
|Romeno|1048|1048|  
|Croata|1.050|1.050|  
|Eslovaco|1051|1051|  
|Slovene|1060|1060|  
|Grego|1032|1032|  
|Búlgaro|1026|1026|  
|Russo|1049|1049|  
|Turco|1055|1055|  
|British English|2057|1033|  
|Estoniano|1061|1061|  
|Letão|1062|1062|  
|Lituano|1063|1063|  
|Português (Brasil)|1046|1046|  
|Chinês tradicional|1028|1028|  
|Coreano|1042|1042|  
|Chinês simplificado|2052|2052|  
|Árabe|1025|1025|  
|Tailandês|1054|1054|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de compatibilidade &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
