---
title: O suporte de tipo de parâmetro com valor de tabela do OLE DB (métodos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
ms.assetid: e3c2a450-8fd4-44cb-93d8-affe1b65c68e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eebe58ccc32e7440505237730b062ff9b6056ef0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411215"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>Suporte ao tipo de parâmetro com valor de tabela OLE DB(Métodos)
  Os seguintes métodos OLE DB padrão dão suporte a parâmetros com valor de tabela:  
  
|Método|Suporte de parâmetro com valor de tabela|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|Usado quando você conhece as informações de tipo de parâmetro com valor de tabela e deseja criar uma instância de um objeto do conjunto de linhas de parâmetro com valor de tabela baseado na informações do tipo.<br /><br /> Para obter mais informações, consulte "Cenário estático" em [criação de conjunto de linhas de parâmetro com valor de tabela](table-valued-parameter-rowset-creation.md).|  
|IOpenRowset::OpenRowset|Usado quando você não conhece as informações de tipo de um parâmetro com valor de tabela e deseja criar uma instância de um objeto do conjunto de linhas de parâmetro com valor de tabela em informações de metadados recuperadas do servidor.<br /><br /> Para obter mais informações, consulte "Cenário dinâmico" na [criação de conjunto de linhas de parâmetro com valor de tabela](table-valued-parameter-rowset-creation.md).|  
|ISSCommandWithParameters::SetParameterInfo|Para especificar um parâmetro de comando de parâmetro com valor de tabela, o consumidor Especifica o tipo do parâmetro como "table" ou "DBTYPE_TABLE" no *pwszName* membro da estrutura DBPARAMBINDINFO. O *ulParamSize* é definido como ~ 0. Para obter mais informações, consulte "Especificação de parâmetro com valor de tabela" na [Executing Commands Containing Table-Valued parâmetros](executing-commands-containing-table-valued-parameters.md).|  
|ISSCommandWithParameters::SetParameterProperties|Define as propriedades específicas dos parâmetros com valor de tabela, como nome do esquema, nome de tipo, ordem de coluna e colunas padrão.<br /><br /> O consumidor Especifica o ordinal do parâmetro em que o *iOrdinal* da estrutura SSPARAMPROPS. O conjunto de propriedades solicitado é DBPROPSET_SQLSERVERPARAMETER.|  
|ISSCommandWithParameters::GetParameterInfo|Obtém os tipos de todos os parâmetros para um comando especificado.<br /><br /> Para parâmetros com valor de tabela, o *wType* campo na estrutura DBPARAMINFO terá o tipo DBTYPE_TABLE. O *ulParamSize* campo será definido como ~ 0 para indicar comprimento desconhecido.|  
|ISSCommandWithParameters::GetParameterProperties|Obtém informações de tipo adicionais para parâmetros do tipo DBTYPE_TABLE.<br /><br /> O consumidor Especifica o ordinal do parâmetro em que o *iOrdinal* membro da estrutura SSPARAMPROPS. O consumidor pode solicitar qualquer uma das propriedades que são listadas na isscommandwithparameters:: SetParameterProperties no conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER.<br /><br /> Como o consumidor não conhece o tipo de parâmetro com valor de tabela, o provedor deve definir o SSPROP_PARAM_TYPE_TYPENAME, SSPROP_PARAM_TYPE_SCHEMANAME e SSPROP_PARAM_TYPE_CATALOGNAME com seus valores corretos. As propriedades restantes, SSPROP_PARAM_TABLE_DEFAULT_COLUMNS e SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER, terão seus valores padrão. Depois que o consumidor descobrir o nome do tipo de parâmetro com valor de tabela, ele usa IOpenRowset:: OPENROWSET para criar uma instância desse parâmetro com valor de tabela, especificando o nome do tipo de parâmetro com valor de tabela. Para obter mais informações, consulte [descoberta do tipo de parâmetro com valor de tabela](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md).|  
|IRowsetInfo::GetProperties|Obtém propriedades de conjunto de linhas de parâmetro com valor de tabela. O consumidor pode usar essas propriedades para montar associações de maneira ideal.|  
|IColumnsRowset::GetColumnsRowset|Recupera informações de metadados sobre uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para parâmetros com valor de tabela, essa mesma interface fornece informações detalhadas de metadados sobre cada coluna, como o seguinte:<br /><br /> -DBCOLUMN_FLAGS indica nulidade pelo bit de DBCOLUMNFLAGS_ISNULLABLE.<br />-DBCOLUMN_ISUNIQUE indica se a coluna é uma coluna de identidade.<br />-DBCOLUMN_COMPUTEMODE indica se a coluna é computada.|  
|IAccessor::CreateAccessor|Para associar um objeto de conjunto de linhas de parâmetro com valor de tabela para um parâmetro de comando, você cria um acessador com seu *wType* membro definido como DBTYPE_TABLE. A estrutura DBOBJECT conterá IID_IRowset ou qualquer outra interface de objeto do conjunto de linhas válido na *iid* membro. O restante dos campos é tratado de forma semelhante a DBTYPE_IUNKNOWN.|  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao tipo de parâmetro com valor de tabela de banco de dados OLE](ole-db-table-valued-parameter-type-support.md)   
 [Criação de conjunto de linhas de parâmetro com valor de tabela](table-valued-parameter-rowset-creation.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)  
  
  
