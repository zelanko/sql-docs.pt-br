---
title: Linhas de DBSCHEMA_COLUMNS | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBSCHEMA_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 32df882f6f6b34c4cd5049713240460c62324ddb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="dbschemacolumns-rowset"></a>Conjunto de linhas de DBSCHEMA_COLUMNS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Fornece informações de coluna para todas as colunas que atendem aos critérios de restrição fornecidos.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DBSCHEMA_COLUMNS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**||O nome do Banco de dados.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**||Sem suporte.|  
|**TABLE_NAME**|**DBTYPE_WSTR**||O nome do cubo.|  
|**NOME DA COLUNA**|**DBTYPE_WSTR**||O nome da hierarquia ou da medida do atributo.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||Sem suporte.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||Sem suporte.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||A posição da coluna, começando por 1.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**||Sem suporte.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||Sem suporte.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||Um **DBCOLUMNFLAGS** bitmask que indica as propriedades de coluna. Consulte 'Tipo enumerado DBCOLUMNFLAGS' em [icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||Sempre retorna **false**.|  
|**DATA_TYPE**|**DBTYPE_WSTR**<br /><br /> **DBTYPE_VARIANT**||O tipo de dados da coluna. Retorna uma cadeia de caracteres para colunas de dimensão e uma variante para medidas.|  
|**TYPE_GUID**|**DBTYPE_GUID**||Sem suporte.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||O comprimento máximo possível de um valor na coluna.<br /><br /> Recuperado por meio de **DataSize** propriedade o **DataItem**.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||O máximo comprimento possível de um valor da coluna, em bytes, para colunas de caractere ou de binários.<br /><br /> Um valor zero (0) indica que a coluna não tem um comprimento máximo.<br /><br /> **NULO** serão retornados para colunas que não retornam tipos de dados de caractere ou binário.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||A precisão máxima da coluna para dados numéricos a tipos diferentes de **DBTYPE_VARNUMERIC**.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||O número de dígitos à direita do ponto decimal para **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, **DBTYPE_VARNUMERIC**. Caso contrário, isso será **nulo**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||Sem suporte.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||Sem suporte.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||Sem suporte.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||Sem suporte.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||Sem suporte.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||Sem suporte.|  
|**COLLATION_NAME**|**DBTYPE_WSTR**||Sem suporte.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||Sem suporte.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||Sem suporte.|  
|**NOME_DO_DOMÍNIO**|**DBTYPE_WSTR**||Sem suporte.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Sem suporte.|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**||O tipo OLAP do objeto.<br /><br /> **MEDIDA** indica o objeto é uma medida.<br /><br /> **ATRIBUTO** indica o objeto é um atributo de dimensão.<br /><br /> **ESQUEMA** indica o objeto é uma coluna em um esquema.|  
  
 O conjunto de linhas é classificado em **TABLE_CATALOG**, **TABLE_SCHEMA**, **TABLE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DBSCHEMA_COLUMNS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**NOME DA COLUNA**|**DBTYPE_WSTR**|Opcional|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas do esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
