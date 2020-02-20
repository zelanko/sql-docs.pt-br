---
title: Suporte ao tipo de parâmetro com valor de tabela OLE DB (Métodos) | Microsoft Docs
description: Suporte ao tipo de parâmetro com valor de tabela OLE DB (Métodos)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d3b8f541956a88361267f54a5dde7a93c9cadc8d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015319"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>Suporte ao tipo de parâmetro com valor de tabela OLE DB(Métodos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os seguintes métodos OLE DB padrão dão suporte a parâmetros com valor de tabela:  
  
|Método|Suporte de parâmetro com valor de tabela|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|Usado quando você conhece as informações de tipo de parâmetro com valor de tabela e deseja criar uma instância de um objeto do conjunto de linhas de parâmetro com valor de tabela baseado na informações do tipo.<br /><br /> Para obter mais informações, confira "Cenário estático" em [Criação do conjunto de linhas do parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md).|  
|IOpenRowset::OpenRowset|Usado quando você não conhece as informações de tipo de um parâmetro com valor de tabela e deseja criar uma instância de um objeto do conjunto de linhas de parâmetro com valor de tabela em informações de metadados recuperadas do servidor.<br /><br /> Para obter mais informações, confira "Cenário dinâmico" em [Criação do conjunto de linhas do parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md).|  
|ISSCommandWithParameters::SetParameterInfo|Para especificar um parâmetro de comando do parâmetro com valor de tabela, o consumidor especifica o tipo de parâmetro como "table" ou "DBTYPE_TABLE" no membro *pwszName* da estrutura DBPARAMBINDINFO. O *ulParamSize* é definido como ~0. Para obter mais informações, confira "Especificação de parâmetros com valor de tabela" em [Como executar comandos que contêm parâmetros com valor de tabela](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md).|  
|ISSCommandWithParameters::SetParameterProperties|Define as propriedades específicas dos parâmetros com valor de tabela, como nome do esquema, nome de tipo, ordem de coluna e colunas padrão.<br /><br /> O consumidor especifica o ordinal do parâmetro no *iOrdinal* da estrutura SSPARAMPROPS. O conjunto de propriedades solicitado é DBPROPSET_SQLSERVERPARAMETER.|  
|ISSCommandWithParameters::GetParameterInfo|Obtém os tipos de todos os parâmetros para um comando especificado.<br /><br /> Para parâmetros com valor de tabela, o campo *wType* na estrutura DBPARAMINFO terá o tipo DBTYPE_TABLE. O campo *ulParamSize* será definido como ~ 0 para indicar comprimento desconhecido.|  
|ISSCommandWithParameters::GetParameterProperties|Obtém informações de tipo adicionais para parâmetros do tipo DBTYPE_TABLE.<br /><br /> O consumidor especifica o ordinal do parâmetro no membro *iOrdinal* da estrutura SSPARAMPROPS. O consumidor pode solicitar qualquer propriedade do conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER listado sob ISSCommandWithParameters::SetParameterProperties.<br /><br /> Como o consumidor não conhece o tipo de parâmetro com valor de tabela, o provedor deve definir o SSPROP_PARAM_TYPE_TYPENAME, SSPROP_PARAM_TYPE_SCHEMANAME e SSPROP_PARAM_TYPE_CATALOGNAME com seus valores corretos. As propriedades restantes, SSPROP_PARAM_TABLE_DEFAULT_COLUMNS e SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER, terão seus valores padrão. Depois que o consumidor descobrir o nome do tipo de parâmetro com valor de tabela, ele usará IOpenRowset::OpenRowset para criar uma instância desse parâmetro com valor de tabela especificando o nome do tipo de parâmetro com valor de tabela. Para obter mais informações, confira [Descoberta de tipo de parâmetros com valor de tabela](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md).|  
|IRowsetInfo::GetProperties|Obtém propriedades de conjunto de linhas de parâmetro com valor de tabela. O consumidor pode usar essas propriedades para montar associações de maneira ideal.|  
|IColumnsRowset::GetColumnsRowset|Recupera informações de metadados sobre uma tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para parâmetros com valor de tabela, essa mesma interface fornece informações detalhadas de metadados sobre cada coluna, como o seguinte:<br /><br /> DBCOLUMN_FLAGS indica nulidade pelo bit de DBCOLUMNFLAGS_ISNULLABLE.<br /><br /> DBCOLUMN_ISUNIQUE indica se a coluna é uma coluna de identidade.<br /><br /> DBCOLUMN_COMPUTEMODE indica se a coluna é computada.|  
|IAccessor::CreateAccessor|Para associar um objeto de conjunto de linhas de parâmetro com valor de tabela a um parâmetro de comando, crie um acessador com seu membro *wType* definido como DBTYPE_TABLE. A estrutura DBOBJECT conterá IID_IRowset ou qualquer outra interface de objeto de conjunto de linhas válida no membro *iid*. O restante dos campos é tratado de forma semelhante a DBTYPE_IUNKNOWN.|  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte para o tipo de parâmetro com valor de tabela do OLE DB](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [Criação do conjunto de linhas do parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
