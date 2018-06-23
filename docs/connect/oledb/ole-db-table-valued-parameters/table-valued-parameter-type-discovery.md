---
title: Descoberta do tipo de parâmetro com valor de tabela | Microsoft Docs
description: Descoberta de tipo de parâmetro com valor de tabela usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 44f763c67c462385cdaf8a91bc8f4648f7c40591
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689049"
---
# <a name="table-valued-parameter-type-discovery"></a>Descoberta do tipo de parâmetro com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O consumidor — ou seja, o aplicativo cliente usando o Driver OLE DB para SQL Server — pode descobrir o tipo de cada parâmetro de comando se o texto do comando tiver sido fornecido ao provedor OLE DB. Depois que o tipo de um parâmetro com valor de tabela for conhecido, o consumidor pode descobrir as informações de metadados para cada coluna individual do parâmetro com valor de tabela.  
  
 As informações de tipo de parâmetros de procedimento tem suporte pelo ICommandWithParameters:: Getparameterinfo para a maioria dos tipos de parâmetro. Começando com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], com a introdução de tipos definidos pelo usuário e o **xml** tipo de dados, o método GetParameterInfo não era suficiente para essa finalidade porque não foi possível fornecer o tipo definido pelo usuário informações (nome, esquema e catálogo) por meio de ICommandWithParameters. Uma nova interface, ISSCommandWithParameters, foi definida para fornecer informações de tipo estendido.  
  
 Para parâmetros com valor de tabela, você também deve usar a interface ISSCommandWithParameters para descobrir informações detalhadas. O cliente chama ISSCommandWithParameters::GetParameterInfo depois de preparar o objeto de comando. Para parâmetros com valor de tabela, o *wType* membro da estrutura DBPARAMINFO é definido como DBTYPE_TABLE pelo provedor. O *ulParamSize* campo da estrutura DBPARAMINFO tem um valor de ~ 0.  
  
 O consumidor solicita então propriedades adicionais (nome de catálogo do tipo de parâmetro com valor de tabela, nome de esquema do tipo de parâmetro com valor de tabela, nome de tipo de parâmetro com valor de tabela, classificação da coluna e colunas padrão) usando ISSCommandWithParamters:: GetParameterProperties.  
  
 Depois que o nome do tipo é conhecido, para recuperar as informações de coluna individual, o consumidor deve chamar IOpenRowset::OpenRowsetor obter o conjunto de linhas DBSCHEMA_TABLE_TYPE_COLUMNS especificando o nome do tipo de parâmetro com valor de tabela como o nome da tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
