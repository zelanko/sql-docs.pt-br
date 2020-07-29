---
title: Descoberta de tipo de parâmetro com valor de tabela | Microsoft Docs
description: Descoberta de tipo de parâmetro com valor de tabela usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 06e0de0ad5fb0b4b8b7fd90144769ca9f9133928
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003336"
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O consumidor, ou seja, o aplicativo cliente que usa o OLE DB Driver para SQL Server, poderá descobrir o tipo de cada parâmetro de comando se o texto do comando tiver sido fornecido ao Provedor do OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados de cada coluna específica do parâmetro com valor de tabela.  
  
 As informações de tipo dos parâmetros de procedimento são compatíveis com ICommandWithParameters::GetParameterInfo para a maioria dos tipos de parâmetro. Começando com o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], com a introdução de tipos definidos pelo usuário e o tipo de dados **xml**, o método GetParameterInfo não era suficiente para essa finalidade, pois não era possível fornecer informações de tipo definido pelo usuário (nome, esquema e catálogo) por meio de ICommandWithParameters. Uma interface nova, a ISSCommandWithParameters, foi definida para fornecer informações de tipo estendidas.  
  
 Para parâmetros com valor de tabela, você também usa a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo após preparar o objeto de comando. Para parâmetros com valor de tabela, o membro *wType* da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O campo *ulParamSize* da estrutura DBPARAMINFO tem um valor de ~0.  
  
 O cliente solicitará as propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome do tipo de parâmetro com valor de tabela, ordenação de colunas e colunas padrão) usando o ISSCommandWithParameters::GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna específicas, o consumidor deve chamar IOpenRowset::OpenRowsetor ou obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como nome da tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
