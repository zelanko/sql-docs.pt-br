---
title: Conjunto de linhas DBSCHEMA_CATALOGS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61e4de1591752919a5916d6044591bda49b14992
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="dbschemacatalogs-rowset"></a>Conjunto de linhas DBSCHEMA_CATALOGS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica os atributos físicos associados a catálogos acessíveis a partir do DBMS (sistema de gerenciamento de banco de dados).  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DBSCHEMA_CATALOGS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|O nome do catálogo. Não pode ser nulo.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição legível da tabela.|  
|**FUNÇÕES**|**DBTYPE_WSTR**||Uma lista de funções delimitadas por vírgulas às quais pertence o usuário atual.<br /><br /> Um asterisco (\*) é incluído como uma função se o usuário atual é um administrador do servidor ou banco de dados.<br /><br /> **Username** é anexado a **ROLES** quando uma das funções usa a segurança dinâmica.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||A data da última modificação do catálogo.|  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DBSCHEMA_CATALOGS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
