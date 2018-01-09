---
title: Conjunto de linhas DBSCHEMA_CATALOGS | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DBSCHEMA_CATALOGS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 493ffd66eb4bcddd0e4aaef7c79c4c771520be92
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="dbschemacatalogs-rowset"></a>Conjunto de linhas DBSCHEMA_CATALOGS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Identifica os atributos físicos associados a catálogos acessíveis a partir do sistema de gerenciamento de banco de dados (DBMS).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas do esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
