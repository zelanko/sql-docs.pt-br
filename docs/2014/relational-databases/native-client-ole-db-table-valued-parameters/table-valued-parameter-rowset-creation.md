---
title: Criação de conjunto de linhas de parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de130ef821551383ada1a6df3574404cd3518e88
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046496"
---
# <a name="table-valued-parameter-rowset-creation"></a>Criação do conjunto de linhas do parâmetro com valor de tabela
  Embora os consumidores possam fornecer qualquer objeto do conjunto de linhas a parâmetros com valor de tabela, objetos do conjunto de linhas típicos são implementados com relação a armazenamentos de dados de back-end e, portanto, fornecem desempenho limitado. Por isso, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite que os consumidores criem um objeto de conjunto de linhas especializado sobre os dados da memória. Esse objeto de conjunto de linhas especiais, na memória é um novo objeto COM chamado um conjunto de linhas de parâmetro com valor de tabela. Ele fornece funcionalidade semelhante para conjuntos de parâmetro.  
  
 Os objetos do conjunto de linhas do parâmetro com valor de tabela são criados explicitamente pelo consumidor para parâmetros de entrada por meio de várias interfaces no nível da sessão. Há uma instância de um objeto do conjunto de linhas do parâmetro com valor de tabela por parâmetro com valor de tabela. O consumidor pode criar os objetos do conjunto de linhas do parâmetro com valor de tabela fornecendo informações de metadados já conhecidas (cenário estático) ou descobrindo-as por meio das interfaces do provedor (cenário dinâmico). As seções a seguir descrevem estes dois cenários.  
  
## <a name="static-scenario"></a>Cenário estático  
 Quando as informações de tipo são conhecidas, o consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para instanciar um objeto de conjunto de linhas de parâmetro com valor de tabela que corresponde a um parâmetro com valor de tabela.  
  
 O *guid* campo (*pTableID* parâmetro) contém a GUID especial (CLSID_ROWSET_TVP). O membro *pwszName* contém o nome do tipo de parâmetro com valor de tabela para o qual o consumidor deseja criar uma instância. O campo *eKind* será definido como DBKIND_GUID_NAME. Esse nome é necessário quando a instrução for ad hoc SQL; o nome é opcional, se for uma chamada de procedimento.  
  
 Para agregação, o consumidor transmite o *pUnkOuter* parâmetro com o controle IUnknown.  
  
 As propriedades de objeto do conjunto de linhas de parâmetro com valor de tabela são somente leitura, portanto, o consumidor não é esperado para definir as propriedades no *rgPropertySets*.  
  
 Para o membro *rgPropertySets* de cada estrutura DBCOLUMNDESC, o consumidor pode especificar propriedades adicionais para cada coluna. Essas propriedades pertencem ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN. Elas permitem que você especifique as configurações computadas e padrão de cada coluna. Elas também dão suporte a propriedades de coluna existentes, como nulidade e identidade.  
  
 Para recuperar informações correspondentes de um objeto do conjunto de linhas do parâmetro com valor de tabela, o consumidor usa IRowsetInfo::GetProperties.  
  
 Para recuperar as informações sobre o nulo, exclusivo, computado e atualizar o status de cada coluna, o consumidor usar IColumnsRowset:: Getcolumnsrowset ou icolumnsinfo:: Getcolumninfo. Esses métodos fornecem informações detalhadas sobre cada coluna do conjunto de linhas do parâmetro com valor de tabela.  
  
 O consumidor especifica o tipo de cada coluna do parâmetro com valor de tabela. Esse procedimento é semelhante à forma de especificação de colunas quando uma tabela é criada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O consumidor obtém um objeto de conjunto de linhas de parâmetro com valor de tabela das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider por meio de *ppRowset* parâmetro de saída.  
  
## <a name="dynamic-scenario"></a>Cenário dinâmico  
 Quando o consumidor não tem informações de tipo, ele deve usar IOpenRowset:: OPENROWSET para instanciar objetos do conjunto de linhas de parâmetro com valor de tabela. O consumidor deve fornecer ao provedor somente o nome do tipo.  
  
 Nesse cenário, o provedor obtém as informações de tipo sobre um objeto do conjunto de linhas do parâmetro com valor de tabela do servidor em nome do consumidor.  
  
 O *pTableID* e *pUnkOuter* parâmetros devem ser definidos como no cenário estático. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider, em seguida, obtém as informações de tipo (informações de coluna e restrições) do servidor e retornar um objeto de conjunto de linhas de parâmetro com valor de tabela por meio de *ppRowset* parâmetro. Esta operação requer comunicação com o servidor e, portanto, não realiza, bem como no cenário estático. O cenário dinâmico só funciona com chamadas de procedimento com parâmetros.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
