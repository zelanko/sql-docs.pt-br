---
title: Mapeamento do tipo de dados em ITableDefinition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3e828efa513db1ace272e59379f77d063220290
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296995"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ao criar tabelas usando a função **ITableDefinition::CreateTable,** o consumidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor DeLE DB cliente nativo pode especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados no membro *pwszTypeName* da matriz DBCOLUMNDESC que é aprovada. Caso o consumidor especifique o tipo de dados de uma coluna por nome, o mapeamento do tipo de dados OLE DB, representado pelo membro *wType* da estrutura DBCOLUMNDESC, será ignorado.  
  
 Ao especificar novos tipos de dados de coluna com os tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB usando o membro *wType* da estrutura DBCOLUMNDESC, o provedor Nativo Cliente OLE DB mapeia os tipos de dados Do LE DB da seguinte forma.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** ou **varbinary(max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB inspeciona o membro *ulColumnSize* da estrutura DBCOLUMNDESC. Com base no valor e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão da instância, o provedor Native Client OLE DB mapeia o tipo de **imagem**.<br /><br /> Se o valor do *ulColumnSize* for menor do que o comprimento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] máximo de uma coluna de tipo de dados **binários,** o provedor Native Client OLE DB inspeciona o membro DBCOLUMNDESC *rgPropertySets.* Se DBPROP_COL_FIXEDLENGTH for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, o provedor Native Client OLE DB mapeia o tipo para **binário**. Se o valor da propriedade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for VARIANT_FALSE, o provedor Cliente Nativo OLE DB mapeia o tipo para **varbinary**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB inspeciona os membros *bPrecision* e *bScale* do DBCOLUMDESC para determinar precisão e escala para a coluna **numérica.**|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** ou **varchar(max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB inspeciona o membro *ulColumnSize* da estrutura DBCOLUMNDESC. Com base no valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão da instância, o provedor Native Client OLE DB mapeia o tipo para **texto**.<br /><br /> Se o valor do *ulColumnSize* for menor do que o comprimento máximo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma coluna de tipo de dados de caracteres multibytes, o provedor Native Client OLE DB inspeciona o membro DBCOLUMNDESC *rgPropertySets.* Se DBPROP_COL_FIXEDLENGTH for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, o provedor Native Client OLE DB mapeia o tipo para **char**. Se o valor da propriedade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for VARIANT_FALSE, o provedor Native Client OLE DB mapeia o tipo para **varchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_UDT|**Udt**|As seguintes informações são usadas em estruturas **DBCOLUMNDESC** por **ITableDefinition::CreateTable** quando as colunas UDT são obrigatórias:<br /><br /> *pwSzTypeName* é ignorado.<br /><br /> *rgPropertySets* deve incluir uma propriedade **DBPROPSET_SQLSERVERCOLUMN** definida conforme descrito na seção sobre **DBPROPSET_SQLSERVERCOLUMN**, em [Uso de tipos definidos pelo usuário](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** ou **nvarchar(max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB inspeciona o membro *ulColumnSize* da estrutura DBCOLUMNDESC. Com base no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valor, o provedor Native Client OLE DB mapeia o tipo para **ntext**.<br /><br /> Se o valor do *ulColumnSize* for menor do que o comprimento máximo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma coluna de tipo de dados de caracteres Unicode, o provedor Native Client OLE DB inspeciona o membro DBCOLUMNDESC *rgPropertySets.* Se DBPROP_COL_FIXEDLENGTH estiver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, o provedor Native Client OLE DB mapeia o tipo para **nchar**. Se o valor da propriedade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for VARIANT_FALSE, o provedor Nativo Cliente OLE DB mapeia o tipo para **nvarchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Ao criar uma nova tabela, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeia apenas os valores de enumeração do tipo de dados OLE DB especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
