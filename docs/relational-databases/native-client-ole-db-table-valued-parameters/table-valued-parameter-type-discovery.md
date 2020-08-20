---
description: Descoberta do tipo de parâmetro com valor de tabela
title: Descoberta de tipo de parâmetro com valor de tabela (provedor de OLE DB de cliente nativo)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 657f380d74d77d1e04d22365a89b34b840279c93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490662"
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O consumidor, ou seja, o aplicativo cliente que usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo – pode descobrir o tipo de cada parâmetro de comando se o texto do comando tiver sido fornecido ao provedor de OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados de cada coluna específica do parâmetro com valor de tabela.  
  
 As informações de tipo dos parâmetros de procedimento são compatíveis com ICommandWithParameters::GetParameterInfo para a maioria dos tipos de parâmetro. Começando com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], com a introdução de tipos definidos pelo usuário e o tipo de dados **xml**, o método GetParameterInfo não era suficiente para essa finalidade, pois não era possível fornecer informações de tipo definido pelo usuário (nome, esquema e catálogo) por meio de ICommandWithParameters. Uma interface nova, a ISSCommandWithParameters, foi definida para fornecer informações de tipo estendidas.  
  
 Para parâmetros com valor de tabela, você também usa a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo após preparar o objeto de comando. Para parâmetros com valor de tabela, o membro *wType* da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O campo *ulParamSize* da estrutura DBPARAMINFO tem um valor de ~0.  
  
 O cliente solicitará as propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome do tipo de parâmetro com valor de tabela, ordenação de colunas e colunas padrão) usando o ISSCommandWithParameters::GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna específicas, o consumidor deve chamar IOpenRowset::OpenRowsetor ou obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como nome da tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
