---
title: Mapeamento de tipo de dados em ITableDefinition | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bdf3a1e716fd1de5354b735e353916bab863059c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73774309"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ao criar tabelas usando a função **ITableDefinition:: CreateTable** , o consumidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode especificar tipos de dados no membro *pwszTypeName* da matriz DBCOLUMNDESC que é passada. Caso o consumidor especifique o tipo de dados de uma coluna por nome, o mapeamento do tipo de dados OLE DB, representado pelo membro *wType* da estrutura DBCOLUMNDESC, será ignorado.  
  
 Ao especificar novos tipos de dados de coluna com OLE DB tipos de dados usando o membro *wType* da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estrutura DBCOLUMNDESC, o provedor de OLE DB do cliente nativo mapeia OLE DB tipos de dados da seguinte maneira.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**Binary**, **varbinary**, **Image** ou **varbinary (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona o membro *ULCOLUMNSIZE* da estrutura DBCOLUMNDESC. Com base no valor e na versão da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo mapeia o tipo para **imagem**.<br /><br /> Se o valor de *ulColumnSize* for menor que o comprimento máximo de uma coluna de tipo de dados **Binary** , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo inspecionará o membro DBCOLUMNDESC *rgPropertySets* . Se DBPROP_COL_FIXEDLENGTH for VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo mapeará o tipo para **binário**. Se o valor da propriedade for VARIANT_FALSE, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo mapeará o tipo para **varbinary**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona os membros DBCOLUMDESC *bPrecision* e *bScale* para determinar a precisão e a escala da coluna **numérica** .|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**Char**, **varchar**, **Text** ou **varchar (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona o membro *ULCOLUMNSIZE* da estrutura DBCOLUMNDESC. Com base no valor e na versão da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo mapeia o tipo para **texto**.<br /><br /> Se o valor de *ulColumnSize* for menor do que o comprimento máximo de uma coluna de tipo de dados de caractere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] multibyte, o provedor de OLE DB de cliente nativo inspecionará o membro DBCOLUMNDESC *rgPropertySets* . Se DBPROP_COL_FIXEDLENGTH for VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo mapeará o tipo para **Char**. Se o valor da propriedade for VARIANT_FALSE, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo mapeará o tipo para **varchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_UDT|**UDT**|As seguintes informações são usadas em estruturas **DBCOLUMNDESC** por **ITableDefinition::CreateTable** quando as colunas UDT são obrigatórias:<br /><br /> *pwszTypeName* é ignorado.<br /><br /> *rgPropertySets* deve incluir um conjunto de propriedades **DBPROPSET_SQLSERVERCOLUMN** conforme descrito na seção em **DBPROPSET_SQLSERVERCOLUMN**, em [usando tipos definidos pelo usuário](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** ou **nvarchar (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inspeciona o membro *ULCOLUMNSIZE* da estrutura DBCOLUMNDESC. Com base no valor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo mapeia o tipo para **ntext**.<br /><br /> Se o valor de *ulColumnSize* for menor do que o comprimento máximo de uma coluna de tipo de dados de caractere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Unicode, o provedor de OLE DB de cliente nativo inspecionará o membro DBCOLUMNDESC *rgPropertySets* . Se DBPROP_COL_FIXEDLENGTH for VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo mapeará o tipo para **nchar**. Se o valor da propriedade for VARIANT_FALSE, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo mapeará o tipo para **nvarchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Ao criar uma nova tabela, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeia apenas os valores de enumeração do tipo de dados OLE DB especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
