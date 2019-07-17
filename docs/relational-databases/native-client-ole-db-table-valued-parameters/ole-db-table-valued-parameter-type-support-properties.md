---
title: Suporte ao tipo de parâmetro com valor de tabela do OLE DB (Propriedades) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
ms.assetid: b9c4e6ed-fe4f-4ef8-9bc8-784d80d44039
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d578fe4b389f9d20d656d43d17c28cd610e3437
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133380"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>Suporte ao tipo de parâmetro com valor de tabela de OLE DB (propriedades)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tópico fornece informações sobre propriedades e conjuntos de propriedades de OLE DB associados a objetos de conjunto de linhas de parâmetro com valor de tabela.  
  
## <a name="properties"></a>Propriedades  
 Veja a seguir a lista de propriedades expostas por meio do método IRowsetInfo::GetProperties em objetos de conjunto de linhas do parâmetro com valor de tabela. Observe que todas as propriedades de conjunto de linhas de parâmetro com valor de tabela são somente leitura. Portanto, tentar definir qualquer uma das propriedades por meio de IOpenRowset:: OPENROWSET ou ITableDefinitionWithConstraints::CreateTableWithConstraints métodos para seus valores não padrão resultará em um erro e nenhum objeto será criado.  
  
 Não estão listadas propriedades não implementadas no objeto de conjunto de linhas de parâmetro com valor de tabela. Para obter uma lista completa de propriedades, consulte a documentação de OLE DB no Windows Data Access Components.  
  
|ID da propriedade|Valor|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W: Somente leitura<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Indicadores não são permitidos em objetos de conjunto de linhas de parâmetro com valor de tabela.|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo,<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> Observação: O objeto de conjunto de linhas de parâmetro com valor de tabela oferece suporte a interfaces IRowsetChange.<br /><br /> Um conjunto de linhas criado usando DBPROP_IRowsetChange igual a VARIANT_TRUE exibe comportamentos de modo de atualização imediatos.<br /><br /> Entretanto, se as colunas BLOB forem associadas como objetos ISequentialStream, o consumidor deverá mantê-las pelo tempo de vida do objeto de conjunto de linhas de parâmetro com valor de tabela.|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &#124; DBPROPVAL_UP_DELETE &#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>Conjuntos de propriedades  
 A propriedade a seguir define parâmetros com valor de tabela de suporte.  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 Essa propriedade é usada pelo consumidor no processo de criação de um objeto de conjunto de linhas de parâmetro com valor de tabela usando ITableDefinitionWithConstraints::CreateTableWithConstraints para cada coluna através da estrutura DBCOLUMNDESC, se necessário.  
  
|ID da propriedade|Valor da propriedade|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W: Leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Digite: VT_BOOL<br /><br /> Descrição: Quando definido como VARIANT_TRUE, indica que a coluna é uma coluna computada. VARIANT_FALSE indica que não é uma coluna computada.|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 Essas propriedades são lidas pelo consumidor ao descobrir as informações de tipo de parâmetro com valor de tabela em chamadas para isscommandwithparameters:: Getparameterproperties e definidas pelo consumidor ao definir propriedades específicas sobre o parâmetro com valor de tabela por meio de isscommandwithparameters:: SetParameterProperties.  
  
 A tabela a seguir fornece descrições detalhadas destas propriedades.  
  
|ID da propriedade|Valor da propriedade|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W: Leitura/gravação<br /><br /> Padrão: VT_EMPTY<br /><br /> Digite: VT_BSTR<br /><br /> Descrição: Os consumidores usam esta propriedade para obter ou definir o nome do tipo de parâmetro com valor de tabela.<br /><br /> Esta propriedade também pode ser usada com tipos de dados CLR definidos pelo usuário.<br /><br /> Esta propriedade pode ser especificada opcionalmente para fornecer um nome de tipo de tabela para um parâmetro com valor de tabela (no caso de comando de sintaxe de chamada ODBC). Esta propriedade é necessária para consultas SQL parametrizadas ad hoc.|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W: Leitura/gravação<br /><br /> Padrão: VT_EMPTY<br /><br /> Digite: VT_BSTR<br /><br /> Descrição: Os consumidores usam esta propriedade para obter ou definir o nome do esquema do tipo de parâmetro com valor de tabela.<br /><br /> Esta propriedade também pode ser usada com tipos de dados CLR definidos pelo usuário.|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W: Somente leitura<br /><br /> Padrão: VT_EMPTY<br /><br /> Digite: VT_BSTR<br /><br /> Descrição: Os consumidores usam esta propriedade para obter o nome do catálogo do tipo de parâmetro com valor de tabela.<br /><br /> Esta propriedade também pode ser usada com tipos de dados CLR definidos pelo usuário. É um erro definir esta propriedade; os tipos de tabela definidos pelo usuário precisam estar no mesmo banco de dados dos parâmetros com valor de tabela que os usam.|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W: Leitura/gravação<br /><br /> Padrão: VT_EMPTY<br /><br /> Digite: VT_UI2 &#124; VT_ARRAY<br /><br /> Descrição: Os consumidores usam esta propriedade para especificar qual conjunto de colunas no conjunto de linhas devem ser tratados como padrões. Nenhum valor será enviado para essas colunas. Ao buscar dados do objeto de conjunto de linhas de consumidor, o provedor não exige uma associação para essas colunas.<br /><br /> Cada elemento da matriz deve ser um ordinal de uma coluna no objeto de conjunto de linhas. Os ordinais inválidos resultarão em erros no momento de execução do comando.|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W: Leitura/gravação<br /><br /> Padrão: VT_EMPTY<br /><br /> Digite: VT_UI2 &#124; VT_ARRAY<br /><br /> Descrição: Essa propriedade é usada pelo consumidor para fornecer uma dica para o servidor para indicar a classificação ordenação dos dados da coluna. O provedor não executa nenhuma validação e pressupõe que o consumidor está de acordo com a especificação fornecida. O servidor usa esta propriedade para executar otimizações.<br /><br /> As informações da ordem de cada coluna são representadas por um par de elementos na matriz. O primeiro elemento do par é o número da coluna. O segundo elemento do par será 1 para ordem crescente ou 2 para decrescente.|  
  
## <a name="see-also"></a>Consulte também  
 [Suporte para o tipo de parâmetro com valor de tabela do OLE DB](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
