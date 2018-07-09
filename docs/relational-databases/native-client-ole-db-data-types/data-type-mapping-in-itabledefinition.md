---
title: Mapeamento de tipo de dados em ITableDefinition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 260b2eab13de427473e92a66f4e97ecdaa077376
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429915"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao criar tabelas usando o **itabledefinition:: CreateTable** função, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client pode especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados no *pwszTypeName* membro da matriz DBCOLUMNDESC passada. Se o consumidor Especifica o tipo de dados de uma coluna por nome, de tipo de dados OLE DB mapeamento, representado pela *wType* membro da estrutura DBCOLUMNDESC, é ignorado.  
  
 Ao especificar novos tipos de dados de coluna com tipos de dados OLE DB usando a estrutura DBCOLUMNDESC *wType* membro, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client mapeia tipos de dados do OLE DB da seguinte maneira.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binário**, **varbinary**, **imagem** ou **varbinary (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor e na versão dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client mapeia o tipo para **imagem**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma **binário** coluna de tipo de dados, em seguida, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inspeciona o DBCOLUMNDESC  *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **binário**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **varbinary**. Em ambos os casos, DBCOLUMNDESC *ulColumnSize* determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona os MEMBROS *bPrecision* e *bScale* membros para determinar a precisão e escala para o **numérico** coluna.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **texto,** ou **varchar (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor de versão dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client mapeia o tipo para **texto**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caractere multibyte, em seguida, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inspeciona o DBCOLUMNDESC *rgPropertySets*membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **char**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **varchar**. Em ambos os casos, DBCOLUMNDESC *ulColumnSize* determina a largura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna criada.|  
|DBTYPE_UDT|**UDT**|As informações a seguir são usadas em **DBCOLUMNDESC** estruturas por **itabledefinition:: CreateTable** quando colunas UDT são obrigatórias:<br /><br /> *pwSzTypeName* será ignorado.<br /><br /> *rgPropertySets* deve incluir uma **DBPROPSET_SQLSERVERCOLUMN** propriedade definida conforme descrito na seção sobre **DBPROPSET_SQLSERVERCOLUMN**, em [Using User-Defined tipos ](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** ou **nvarchar (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **ntext**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caractere Unicode, em seguida, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inspeciona o DBCOLUMNDESC *rgPropertySets*membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **nchar**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **nvarchar**. Em ambos os casos, DBCOLUMNDESC *ulColumnSize* determina a largura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna criada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Ao criar uma nova tabela, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeia apenas os valores de enumeração do tipo de dados OLE DB especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
