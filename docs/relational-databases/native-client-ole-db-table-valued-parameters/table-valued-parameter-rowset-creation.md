---
title: Criação do conjunto de linhas do parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab3541f354af26f32f4071c2a6d09648cd53af6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283072"
---
# <a name="table-valued-parameter-rowset-creation"></a>Criação do conjunto de linhas do parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Embora os consumidores possam fornecer qualquer objeto do conjunto de linhas a parâmetros com valor de tabela, objetos do conjunto de linhas típicos são implementados com relação a armazenamentos de dados de back-end e, portanto, fornecem desempenho limitado. Por isso, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite que os consumidores criem um objeto de conjunto de linhas especializado sobre os dados da memória. Este objeto especial de conjunto de linhas na memória é um novo objeto COM chamado de conjunto de linhas de parâmetro sumido por tabela . Ele fornece funcionalidade semelhante para conjuntos de parâmetro.  
  
 Os objetos do conjunto de linhas do parâmetro com valor de tabela são criados explicitamente pelo consumidor para parâmetros de entrada por meio de várias interfaces no nível da sessão. Há uma instância de um objeto do conjunto de linhas do parâmetro com valor de tabela por parâmetro com valor de tabela. O consumidor pode criar os objetos do conjunto de linhas do parâmetro com valor de tabela fornecendo informações de metadados já conhecidas (cenário estático) ou descobrindo-as por meio das interfaces do provedor (cenário dinâmico). As seções a seguir descrevem estes dois cenários.  
  
## <a name="static-scenario"></a>Cenário estático  
 Quando as informações de tipo são conhecidas, o consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para criar uma instância de um conjunto de linhas do parâmetro com valor de tabela que corresponda a um parâmetro com valor de tabela.  
  
 O campo *guid* (parâmetro *pTableID*) contém a GUID especial (CLSID_ROWSET_TVP). O membro *pwszName* contém o nome do tipo de parâmetro com valor de tabela para o qual o consumidor deseja criar uma instância. O campo *eKind* será definido como DBKIND_GUID_NAME. Esse nome é necessário quando a instrução for ad hoc SQL; o nome é opcional, se for uma chamada de procedimento.  
  
 Para agregação, o consumidor transmite o parâmetro *pUnkOuter* com o controlador IUnknown.  
  
 As propriedades do objeto de conjunto de linhas de parâmetro de valor de tabela são somente lidas, de modo que o consumidor não deverá definir quaisquer propriedades em *rgPropertySets*.  
  
 Para o membro *rgPropertySets* de cada estrutura DBCOLUMNDESC, o consumidor pode especificar propriedades adicionais para cada coluna. Essas propriedades pertencem ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN. Elas permitem que você especifique as configurações computadas e padrão de cada coluna. Elas também dão suporte a propriedades de coluna existentes, como nulidade e identidade.  
  
 Para recuperar informações correspondentes de um objeto do conjunto de linhas do parâmetro com valor de tabela, o consumidor usa IRowsetInfo::GetProperties.  
  
 Para recuperar informações sobre o status nulo, único, computado e atualizado de cada coluna, o consumidor usa IColumnsRowset::GetColumnsRowset ou IColumnsInfo::GetColumnInfo. Esses métodos fornecem informações detalhadas sobre cada coluna do conjunto de linhas do parâmetro com valor de tabela.  
  
 O consumidor especifica o tipo de cada coluna do parâmetro com valor de tabela. Esse procedimento é semelhante à forma de especificação de colunas quando uma tabela é criada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O consumidor obtém um objeto de conjunto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de linha de parâmetro de valor de tabela do Provedor De Cliente Nativo OLE DB através do parâmetro de saída *ppRowset.*  
  
## <a name="dynamic-scenario"></a>Cenário dinâmico  
 Quando o consumidor não tiver informações de tipo, ele deve usar IOpenRowset::OpenRowset para agendar objetos de conjunto de parâmetros de tabela. O consumidor deve fornecer ao provedor somente o nome do tipo.  
  
 Nesse cenário, o provedor obtém as informações de tipo sobre um objeto do conjunto de linhas do parâmetro com valor de tabela do servidor em nome do consumidor.  
  
 Os parâmetros *pTableID* e *pUnkOuter* devem ser definidos como no cenário estático. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provedor De Cliente Nativo OLE DB obtém então as informações de tipo (informações da coluna e as restrições) do servidor e retorna um objeto de conjunto de parâmetros de valor de tabela através do parâmetro *ppRowset.* Essa operação requer comunicação com o servidor e, portanto, não tem desempenho tão bom quanto no cenário estático. O cenário dinâmico só funciona com chamadas de procedimento com parâmetros.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros avaliados em tabela &#40;o le DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
