---
title: Descoberta do tipo de parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bdf4acafd0a1bd2d986bbc75f5b1486d7dbb524b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532418"
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
  O consumidor – isto é, o aplicativo cliente usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client – pode descobrir o tipo de cada parâmetro de comando se o texto do comando recebeu para o provedor OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados de cada coluna específica do parâmetro com valor de tabela.  
  
 As informações de tipo dos parâmetros de procedimento há suporte para ICommandWithParameters:: Getparameterinfo para a maioria dos tipos de parâmetro. Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], com a introdução de tipos definidos pelo usuário e o `xml` tipo de dados, o método GetParameterInfo não era suficiente para essa finalidade porque não foi possível fornecer informações de tipo definido pelo usuário (nome, esquema, e catálogo) por meio de ICommandWithParameters. Uma nova interface, ISSCommandWithParameters, foi definida para fornecer informações de tipo estendido.  
  
 Para parâmetros com valor de tabela, você também deve usar a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo depois de preparar o objeto de comando. Para parâmetros com valor de tabela, o membro *wType* da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O campo *ulParamSize* da estrutura DBPARAMINFO tem um valor de ~0.  
  
 O cliente solicitará as propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome do tipo de parâmetro com valor de tabela, ordenação de colunas e colunas padrão) usando o ISSCommandWithParameters::GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna específicas, o consumidor deve chamar IOpenRowset::OpenRowsetor ou obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como nome da tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
