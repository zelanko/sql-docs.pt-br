---
title: Criação de conjunto de linhas de parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c7202570f46ac3ba8045ab825ddd1874f64dd6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="table-valued-parameter-rowset-creation"></a>Criação do conjunto de linhas do parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Embora os consumidores possam fornecer qualquer objeto do conjunto de linhas a parâmetros com valor de tabela, objetos do conjunto de linhas típicos são implementados com relação a armazenamentos de dados de back-end e, portanto, fornecem desempenho limitado. Por isso, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite que os consumidores criem um objeto de conjunto de linhas especializado sobre os dados da memória. Esse objeto de conjunto de linhas especiais, de memória é um novo objeto COM chamado de um conjunto de linhas de parâmetro com valor de tabela. Ele fornece funcionalidade semelhante para conjuntos de parâmetro.  
  
 Os objetos do conjunto de linhas do parâmetro com valor de tabela são criados explicitamente pelo consumidor para parâmetros de entrada por meio de várias interfaces no nível da sessão. Há uma instância de um objeto do conjunto de linhas do parâmetro com valor de tabela por parâmetro com valor de tabela. O consumidor pode criar os objetos do conjunto de linhas do parâmetro com valor de tabela fornecendo informações de metadados já conhecidas (cenário estático) ou descobrindo-as por meio das interfaces do provedor (cenário dinâmico). As seções a seguir descrevem estes dois cenários.  
  
## <a name="static-scenario"></a>Cenário estático  
 Quando as informações de tipo são conhecidas, o consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para instanciar um objeto de conjunto de linhas de parâmetro com valor de tabela que corresponde a um parâmetro com valor de tabela.  
  
 O *guid* campo (*pTableID* parâmetro) contém o GUID especial (CLSID_ROWSET_TVP). O *pwszName* membro contém o nome do tipo de parâmetro com valor de tabela que o consumidor deseja criar uma instância. O *eKind* campo será definido como DBKIND_GUID_NAME. Esse nome é necessário quando a instrução for ad hoc SQL; o nome é opcional, se for uma chamada de procedimento.  
  
 Para agregação, o consumidor transmite o *pUnkOuter* parâmetro com o IUnknown controlador.  
  
 As propriedades de objeto do conjunto de linhas de parâmetro com valor de tabela são somente leitura, portanto não é esperado que o consumidor defina propriedades em *rgPropertySets*.  
  
 Para o *rgPropertySets* membro de cada estrutura DBCOLUMNDESC, o consumidor pode especificar propriedades adicionais para cada coluna. Essas propriedades pertencem ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN. Elas permitem que você especifique as configurações computadas e padrão de cada coluna. Elas também dão suporte a propriedades de coluna existentes, como nulidade e identidade.  
  
 Para recuperar informações correspondentes de um objeto de conjunto de linhas de parâmetro com valor de tabela, o consumidor usa irowsetinfo:: GetProperties.  
  
 Para recuperar as informações sobre o nulo, exclusivo, computado e atualizar o status de cada coluna, o consumidor usar Getcolumnsrowset ou icolumnsinfo:: Getcolumninfo. Esses métodos fornecem informações detalhadas sobre cada coluna do conjunto de linhas do parâmetro com valor de tabela.  
  
 O consumidor especifica o tipo de cada coluna do parâmetro com valor de tabela. Esse procedimento é semelhante à forma de especificação de colunas quando uma tabela é criada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O consumidor obtém um objeto de conjunto de linhas de parâmetro com valor de tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider por meio de *ppRowset* parâmetro de saída.  
  
## <a name="dynamic-scenario"></a>Cenário dinâmico  
 Quando o consumidor não tem informações de tipo, ele deve usar IOpenRowset:: OPENROWSET para instanciar objetos de conjunto de linhas de parâmetro com valor de tabela. O consumidor deve fornecer ao provedor somente o nome do tipo.  
  
 Nesse cenário, o provedor obtém as informações de tipo sobre um objeto do conjunto de linhas do parâmetro com valor de tabela do servidor em nome do consumidor.  
  
 O *pTableID* e *pUnkOuter* parâmetros devem ser definidos como no cenário estático. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider obtém as informações de tipo (informações de coluna e restrições) do servidor e retornar um objeto de conjunto de linhas de parâmetro com valor de tabela por meio de *ppRowset* parâmetro. Esta operação requer comunicação com o servidor e, portanto, não executa, bem como no cenário estático. O cenário dinâmico só funciona com chamadas de procedimento com parâmetros.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar com valor de tabela parâmetros & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
