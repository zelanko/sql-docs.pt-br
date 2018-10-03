---
title: Mapeamento de tipo de dados em ITableDefinition | Microsoft Docs
description: Mapeamento de tipos de dados em ITableDefinition
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 4101c458b066ec34f010a5733510fb21e25e6840
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834184"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Ao criar tabelas usando a função **ITableDefinition::CreateTable**, o consumidor do OLE DB Driver for SQL Server pode especificar tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no membro *pwszTypeName* da matriz DBCOLUMNDESC passada. Caso o consumidor especifique o tipo de dados de uma coluna por nome, o mapeamento do tipo de dados OLE DB, representado pelo membro *wType* da estrutura DBCOLUMNDESC, será ignorado.  
  
 Ao especificar novos tipos de dados de coluna com tipos de dados OLE DB usando o membro *wType* da estrutura DBCOLUMNDESC, o OLE DB Driver for SQL Server mapeia os tipos de dados do OLE DB conforme mostrado a seguir.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** ou **varbinary(max)**|O Driver do OLE DB para SQL Server inspeciona as *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor e na versão dos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da instância, o Driver do OLE DB para SQL Server mapeia o tipo para **imagem**.<br /><br /> Caso o valor de *ulColumnSize* seja menor que o tamanho máximo de uma coluna de tipo de dados **binary**, o OLE DB Driver for SQL Server inspecionará o membro *rgPropertySets* de DBCOLUMNDESC. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o Driver do OLE DB para SQL Server mapeia o tipo para **binário**. Se o valor da propriedade seja VARIANT_FALSE, o Driver do OLE DB para SQL Server mapeia o tipo para **varbinary**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|O OLE DB Driver for SQL Server inspeciona os membros *bPrecision* e *bScale* de DBCOLUMDESC para determinar a precisão e a escala da coluna **numeric**.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** ou **varchar(max)**|O Driver do OLE DB para SQL Server inspeciona as *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor de versão dos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da instância, o Driver do OLE DB para SQL Server mapeia o tipo para **texto**.<br /><br /> Caso o valor de *ulColumnSize* seja menor que o tamanho máximo de uma coluna de tipo de dados de caractere multibyte, o OLE DB Driver for SQL Server inspecionará o membro *rgPropertySets* de DBCOLUMNDESC. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o Driver do OLE DB para SQL Server mapeia o tipo para **char**. Se o valor da propriedade seja VARIANT_FALSE, o Driver do OLE DB para SQL Server mapeia o tipo para **varchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_UDT|**UDT**|As seguintes informações são usadas em estruturas **DBCOLUMNDESC** por **ITableDefinition::CreateTable** quando as colunas UDT são obrigatórias:<br /><br /> *pwSzTypeName* será ignorado.<br /><br /> *rgPropertySets* deve incluir uma **DBPROPSET_SQLSERVERCOLUMN** propriedade definida conforme descrito na seção sobre **DBPROPSET_SQLSERVERCOLUMN**, em [Using User-Defined tipos ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** ou **nvarchar(max)**|O Driver do OLE DB para SQL Server inspeciona as *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor, o Driver do OLE DB para SQL Server mapeia o tipo para **ntext**.<br /><br /> Caso o valor de *ulColumnSize* seja menor que o tamanho máximo de uma coluna de tipo de dados de caractere Unicode, o OLE DB Driver for SQL Server inspecionará o membro *rgPropertySets* de DBCOLUMNDESC. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o Driver do OLE DB para SQL Server mapeia o tipo para **nchar**. Se o valor da propriedade seja VARIANT_FALSE, o Driver do OLE DB para SQL Server mapeia o tipo para **nvarchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  Ao criar uma nova tabela, o OLE DB Driver for SQL Server mapeia apenas os valores de enumeração do tipo de dados OLE DB especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  

## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
