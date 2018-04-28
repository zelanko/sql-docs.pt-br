---
title: Descoberta do tipo de parâmetro com valor de tabela | Microsoft Docs
description: Descoberta de tipo de parâmetro com valor de tabela usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87d6bf89729f27a9b0e75b9abe92891d2dbb8d1f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O consumidor — ou seja, o aplicativo cliente usando o Driver OLE DB para SQL Server — pode descobrir o tipo de cada parâmetro de comando se o texto do comando tiver sido fornecido ao provedor OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados para cada coluna individual do parâmetro com valor de tabela.  
  
 As informações de tipo de parâmetros de procedimento tem suporte pelo ICommandWithParameters:: Getparameterinfo para a maioria dos tipos de parâmetro. Começando com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], com a introdução de tipos definidos pelo usuário e o **xml** tipo de dados, o método GetParameterInfo não era suficiente para essa finalidade porque não foi possível fornecer o tipo definido pelo usuário informações (nome, esquema e catálogo) por meio de ICommandWithParameters. Uma nova interface, ISSCommandWithParameters, foi definida para fornecer informações de tipo estendido.  
  
 Para parâmetros com valor de tabela, você também deve usar a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo depois de preparar o objeto de comando. Para parâmetros com valor de tabela, o *wType* membro da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O *ulParamSize* campo da estrutura DBPARAMINFO tem um valor de ~ 0.  
  
 O consumidor solicita então propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome de tipo de parâmetro com valor de tabela, classificação da coluna e colunas padrão) usando ISSCommandWithParamters:: GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna individual, o consumidor deve chamar IOpenRowset::OpenRowsetor obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como o nome da tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar com valor de tabela parâmetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
