---
title: Descoberta de tipo de parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cf3f7b4d6754902ac38172ffa0e8fc392599d307
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62780315"
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
  O consumidor, ou seja, o aplicativo cliente que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo – pode descobrir o tipo de cada parâmetro de comando se o texto do comando tiver sido fornecido ao provedor de OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados de cada coluna específica do parâmetro com valor de tabela.  
  
 As informações de tipo dos parâmetros de procedimento são compatíveis com ICommandWithParameters::GetParameterInfo para a maioria dos tipos de parâmetro. Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]o, com a introdução de tipos definidos pelo usuário e `xml` o tipo de dados, o método GetParameterInfo não era suficiente para essa finalidade porque não era possível fornecer informações de tipo definido pelo usuário (nome, esquema e catálogo) por meio de ICommandWithParameters. Uma interface nova, a ISSCommandWithParameters, foi definida para fornecer informações de tipo estendidas.  
  
 Para parâmetros com valor de tabela, você também usa a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo após preparar o objeto de comando. Para parâmetros com valor de tabela, o membro *wType* da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O campo *ulParamSize* da estrutura DBPARAMINFO tem um valor de ~0.  
  
 O cliente solicitará as propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome do tipo de parâmetro com valor de tabela, ordenação de colunas e colunas padrão) usando o ISSCommandWithParameters::GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna específicas, o consumidor deve chamar IOpenRowset::OpenRowsetor ou obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como nome da tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Os parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
