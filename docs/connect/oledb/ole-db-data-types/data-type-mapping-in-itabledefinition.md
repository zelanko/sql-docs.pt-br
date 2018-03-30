---
title: Mapeamento de tipo de dados em ITableDefinition | Microsoft Docs
description: Mapeamento de tipo de dados em ITableDefinition
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34c222d455be68ab8ce96d343593a80f66c94d7d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ao criar tabelas usando o **itabledefinition:: CreateTable** função, o Driver OLE DB para o consumidor do SQL Server pode especificar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados no *pwszTypeName* membro das Matriz DBCOLUMNDESC passada. Se o consumidor Especifica o tipo de dados de uma coluna por nome, de tipo de dados OLE DB mapeamento, representado pelo *wType* membro da estrutura DBCOLUMNDESC, é ignorado.  
  
 Ao especificar novos tipos de dados de coluna com tipos de dados de OLE DB usando a estrutura DBCOLUMNDESC *wType* membro, o Driver OLE DB para SQL Server mapeia tipos de dados OLE DB da seguinte maneira.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binário**, **varbinary**, **imagem,** ou **varbinary (max)**|O Driver OLE DB para SQL Server inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor e na versão da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância, o Driver OLE DB para SQL Server mapeia o tipo para **imagem**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de um **binário** coluna, tipo de dados, em seguida, o Driver OLE DB para SQL Server inspeciona o membro *rgPropertySets*membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o Driver OLE DB para SQL Server mapeia o tipo para **binário**. Se o valor da propriedade seja VARIANT_FALSE, o Driver OLE DB para SQL Server mapeia o tipo para **varbinary**. Em ambos os casos, o membro *ulColumnSize* membro determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|O Driver OLE DB para SQL Server inspeciona os MEMBROS *bPrecision* e *bScale* membros para determinar a precisão e escala para o **numérico** coluna.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **texto,** ou **varchar (max)**|O Driver OLE DB para SQL Server inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor de versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância, o Driver OLE DB para SQL Server mapeia o tipo para **texto**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caracteres multibyte e, em seguida, o Driver OLE DB para SQL Server inspeciona o membro *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o Driver OLE DB para SQL Server mapeia o tipo para **char**. Se o valor da propriedade seja VARIANT_FALSE, o Driver OLE DB para SQL Server mapeia o tipo para **varchar**. Em ambos os casos, o membro *ulColumnSize* membro determina a largura do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] coluna criada.|  
|DBTYPE_UDT|**UDT**|As informações a seguir são usadas em **DBCOLUMNDESC** estruturas por **itabledefinition:: CreateTable** quando colunas UDT são necessárias:<br /><br /> *pwSzTypeName* is ignored.<br /><br /> *rgPropertySets* deve incluir um **DBPROPSET_SQLSERVERCOLUMN** propriedade definida conforme descrito na seção sobre **DBPROPSET_SQLSERVERCOLUMN**, na [Using User-Defined tipos ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** ou **nvarchar (max)**|O Driver OLE DB para SQL Server inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor, o Driver OLE DB para SQL Server mapeia o tipo para **ntext**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caractere Unicode e, em seguida, o Driver OLE DB para SQL Server inspeciona o membro *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o Driver OLE DB para SQL Server mapeia o tipo para **nchar**. Se o valor da propriedade seja VARIANT_FALSE, o Driver OLE DB para SQL Server mapeia o tipo para **nvarchar**. Em ambos os casos, o membro *ulColumnSize* membro determina a largura do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] coluna criada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Ao criar uma nova tabela, o Driver OLE DB para SQL Server mapeia apenas os OLE DB tipo enumeração valores de dados especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40; OLE DB &#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
