---
title: Criação de conjunto de linhas de parâmetro com valor de tabela | Microsoft Docs
description: Criação de conjunto de linhas de parâmetro estática e dinâmica
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b756e3573af050f1fd998c0861308855e456bd10
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307425"
---
# <a name="table-valued-parameter-rowset-creation"></a>Criação do conjunto de linhas do parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Embora os consumidores possam fornecer qualquer objeto do conjunto de linhas a parâmetros com valor de tabela, objetos do conjunto de linhas típicos são implementados com relação a armazenamentos de dados de back-end e, portanto, fornecem desempenho limitado. Por esse motivo, o Driver OLE DB para SQL Server permite que os consumidores criem um objeto de conjunto de linhas especializado sobre os dados na memória. Esse objeto do conjunto de linhas especial na memória é um novo objeto COM denominado conjunto de linhas do parâmetro com valor de tabela. Ele fornece funcionalidade semelhante para conjuntos de parâmetro.  
  
 Os objetos do conjunto de linhas do parâmetro com valor de tabela são criados explicitamente pelo consumidor para parâmetros de entrada por meio de várias interfaces no nível da sessão. Há uma instância de um objeto de conjunto de linhas de parâmetro com valor de tabela por parâmetro com valor de tabela. O consumidor pode criar os objetos do conjunto de linhas do parâmetro com valor de tabela fornecendo informações de metadados já conhecidas (cenário estático) ou descobrindo-as por meio das interfaces do provedor (cenário dinâmico). As seções a seguir descrevem estes dois cenários.  
  
## <a name="static-scenario"></a>Cenário estático  
 Quando as informações de tipo são conhecidas, o consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para instanciar um objeto de conjunto de linhas de parâmetro com valor de tabela que corresponde a um parâmetro com valor de tabela.  
  
 O *guid* campo (*pTableID* parâmetro) contém o GUID especial (CLSID_ROWSET_TVP). O *pwszName* membro contém o nome do tipo de parâmetro com valor de tabela que o consumidor deseja criar uma instância. O *eKind* campo será definido como DBKIND_GUID_NAME. Esse nome é necessário quando a instrução SQL ad hoc; o nome é opcional, se for uma chamada de procedimento.  
  
 Para agregação, o consumidor transmite o *pUnkOuter* parâmetro com o IUnknown controlador.  
  
 As propriedades de objeto do conjunto de linhas de parâmetro com valor de tabela são somente leitura, portanto não se espera que o consumidor defina propriedades *rgPropertySets*.  
  
 Para o *rgPropertySets* membro de cada estrutura DBCOLUMNDESC, o consumidor pode especificar propriedades adicionais para cada coluna. Essas propriedades pertencem ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN. Elas permitem que você especifique as configurações computadas e padrão de cada coluna. Elas também dão suporte a propriedades de coluna existentes, como nulidade e identidade.  
  
 Para recuperar informações correspondentes de um objeto de conjunto de linhas de parâmetro com valor de tabela, o consumidor usa irowsetinfo:: GetProperties.  
  
 Para recuperar as informações sobre o nulo, exclusivo, computado e atualizar o status de cada coluna, o consumidor pode usar Getcolumnsrowset ou icolumnsinfo:: Getcolumninfo. Esses métodos fornecem informações detalhadas sobre cada coluna do conjunto de linhas do parâmetro com valor de tabela.  
  
 O consumidor especifica o tipo de cada coluna do parâmetro com valor de tabela. Ele é semelhante a como as colunas são especificadas quando uma tabela é criada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O consumidor obtém um objeto de conjunto de linhas de parâmetro com valor de tabela do Driver OLE DB para SQL Server por meio de *ppRowset* parâmetro de saída.  
  
## <a name="dynamic-scenario"></a>Cenário dinâmico  
 Quando o consumidor não tem informações de tipo, ele deve usar IOpenRowset:: OPENROWSET para instanciar objetos de conjunto de linhas de parâmetro com valor de tabela. O consumidor deve fornecer ao provedor somente o nome do tipo.  
  
 Nesse cenário, o provedor obtém as informações de tipo sobre um objeto do conjunto de linhas do parâmetro com valor de tabela do servidor em nome do consumidor.  
  
 O *pTableID* e *pUnkOuter* parâmetros devem ser definidos como no cenário estático. O Driver OLE DB para SQL Server, em seguida, obtém as informações de tipo (informações de coluna e restrições) do servidor e retornar um objeto de conjunto de linhas de parâmetro com valor de tabela por meio de *ppRowset* parâmetro. Esta operação requer comunicação com o servidor e, portanto, não executa, bem como no cenário estático. O cenário dinâmico só funciona com chamadas de procedimento com parâmetros.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
