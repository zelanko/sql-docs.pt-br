---
title: Comandos com parâmetros com valor de tabela
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 85dfdf19da0187832fcec316099688d2807de65b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246769"
---
# <a name="executing-sql-server-native-client-commands-containing-table-valued-parameters"></a>Executando comandos de SQL Server Native Client que contêm parâmetros com valor de tabela
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A execução de um comando que contém parâmetros com valor de tabela exige duas fases:  
  
1.  Especificar os tipos de parâmetros.  
  
2.  Associar os dados de parâmetro.  

## <a name="table-valued-parameter-specification"></a>Especificação de parâmetros com valor de tabela  
 O consumidor pode especificar o tipo do parâmetro com valor de tabela. Estas informações incluem o nome do tipo de parâmetro com valor de tabela. Elas também incluem o nome do esquema, se o tipo de tabela definido pelo usuário para o parâmetro com valor de tabela não estiver no esquema padrão atual para a conexão. Dependendo do suporte do servidor, o consumidor também pode especificar informações de metadados opcionais, como a classificação de colunas, e pode especificar que todas as linhas de determinadas colunas tenham os valores padrão.  
  
 Para especificar um parâmetro com valor de tabela, o consumidor chama ISSCommandWithParameter::SetParameterInfo e, opcionalmente, chama ISSCommandWithParameters::SetParameterProperties. Para um parâmetro com valor de tabela, o campo *pwszDataSourceType* na estrutura DBPARAMBINDINFO tem um valor DBTYPE_TABLE. O campo *ulParamSize* é definido como ~0 para indicar que esse tamanho é desconhecido. As propriedades específicas de parâmetros com valor de tabela, como o nome do esquema, o nome do tipo, a ordem das colunas e as colunas padrão, podem ser definidas por meio de ISSCommandWithParameters::SetParameterProperties.  
  
## <a name="table-valued-parameter-binding"></a>Associação de parâmetros com valor de tabela  
 Um parâmetro com valor de tabela pode ser qualquer objeto de conjunto de linhas. O provedor faz a leitura a partir deste objeto enquanto envia parâmetros com valor de tabela ao servidor durante a execução.  
  
 Para associar o parâmetro com valor de tabela, o consumidor chama IAccessor::CreateAccessor. O campo *wType* da estrutura DBBINDING para o parâmetro com valor de tabela é definido como DBTYPE_TABLE. O membro *pObject* da estrutura DBBINDING é não NULL, e o membro *iid* de *pObject* é definido como IID_IRowset ou como qualquer outra interface de objetos de conjunto de linhas do parâmetro com valor de tabela. Os campos restantes na estrutura DBBINDING devem ser definidos da mesma forma que são definidos para BLOBs transmitidos.  
  
 Nas associações para o parâmetro com valor de tabela e o objeto de conjunto de linhas associado a um parâmetro com valor de tabela, as seguintes restrições se aplicam:  
  
-   Os únicos valores de status permitidos para dados da coluna do conjunto de linhas do parâmetro com valor de tabela são DBSTATUS_S_ISNULL e DBSTATUS_S_OK. DBSTATUS_S_DEFAULT resultará em falha e o valor de status associado será definido como DBSTATUS_E_BADSTATUS.  
  
-   Um parâmetro com valor de tabela pode ser marcado com o status DBSTATUS_S_DEFAULT. Os únicos valores válidos são DBSTATUS_S_DEFAULT e DBSTATUS_S_OK. Quando o status é definido como DBSTATUS_S_DEFAULT, o valor do parâmetro com valor de tabela corresponde a uma tabela vazia.  
  
-   As colunas somente leitura em parâmetros com valor de tabela (colunas de identidade ou computadas) devem ser marcadas como padrão usando a propriedade SSPROP_PARAM_TABLE_DEFAULT_COLUMNS. As colunas com um valor padrão também devem ser marcadas como padrão por meio da propriedade SSPROP_PARAM_TABLE_DEFAULT_COLUMNS de forma a permitir que o valor padrão seja usado para os valores de dados da coluna para um determinado parâmetro com valor de tabela. O provedor irá ignorar os valores de dados associados com as colunas marcadas como padrão.  
  
-   Os dados serão enviados ao servidor para colunas com DBPROP_COL_AUTOINCREMENT ou SSPROP_COL_COMPUTED, a menos que SSPROP_PARAM_TABLE_DEFAULT também esteja definido.  
  
## <a name="see-also"></a>Consulte Também  
 [Os parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
