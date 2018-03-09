---
title: "Descoberta do tipo de parâmetro com valor de tabela | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cb2c68a50c97ca1e51dea778c81c5b9d5c60737
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O consumidor — ou seja, o aplicativo cliente usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider – pode descobrir o tipo de cada parâmetro de comando se o texto do comando tiver sido fornecido ao provedor OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados para cada coluna individual do parâmetro com valor de tabela.  
  
 As informações de tipo de parâmetros de procedimento tem suporte pelo ICommandWithParameters:: Getparameterinfo para a maioria dos tipos de parâmetro. Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], com a introdução de tipos definidos pelo usuário e o **xml** tipo de dados, o método GetParameterInfo não era suficiente para essa finalidade porque não foi possível fornecer o tipo definido pelo usuário informações (nome, esquema e catálogo) por meio de ICommandWithParameters. Uma nova interface, ISSCommandWithParameters, foi definida para fornecer informações de tipo estendido.  
  
 Para parâmetros com valor de tabela, você também deve usar a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo depois de preparar o objeto de comando. Para parâmetros com valor de tabela, o *wType* membro da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O *ulParamSize* campo da estrutura DBPARAMINFO tem um valor de ~ 0.  
  
 O consumidor solicita então propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome de tipo de parâmetro com valor de tabela, classificação da coluna e colunas padrão) usando ISSCommandWithParamters:: GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna individual, o consumidor deve chamar IOpenRowset::OpenRowsetor obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como o nome da tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Com valor de tabela parâmetros &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar com valor de tabela parâmetros &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
