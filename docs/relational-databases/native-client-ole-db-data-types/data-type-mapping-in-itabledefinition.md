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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7dcb415dccd20eb2e6ccdfeb894a58fc8431b671
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852094"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao criar tabelas usando o **itabledefinition:: CreateTable** função, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client pode especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados no *pwszTypeName* membro da matriz DBCOLUMNDESC passada. Caso o consumidor especifique o tipo de dados de uma coluna por nome, o mapeamento do tipo de dados OLE DB, representado pelo membro *wType* da estrutura DBCOLUMNDESC, será ignorado.  
  
 Ao especificar novos tipos de dados de coluna com tipos de dados OLE DB usando a estrutura DBCOLUMNDESC *wType* membro, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client mapeia tipos de dados do OLE DB da seguinte maneira.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image,** ou **varbinary(max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor e na versão dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client mapeia o tipo para **imagem**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma **binário** coluna de tipo de dados, em seguida, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inspeciona o DBCOLUMNDESC  *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **binário**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **varbinary**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona os MEMBROS *bPrecision* e *bScale* membros para determinar a precisão e escala para o **numérico** coluna.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** ou **varchar(max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor de versão dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client mapeia o tipo para **texto**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caractere multibyte, em seguida, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inspeciona o DBCOLUMNDESC *rgPropertySets*membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **char**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **varchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_UDT|**UDT**|As seguintes informações são usadas em estruturas **DBCOLUMNDESC** por **ITableDefinition::CreateTable** quando as colunas UDT são obrigatórias:<br /><br /> *pwSzTypeName* será ignorado.<br /><br /> *rgPropertySets* deve incluir uma **DBPROPSET_SQLSERVERCOLUMN** propriedade definida conforme descrito na seção sobre **DBPROPSET_SQLSERVERCOLUMN**, em [Using User-Defined tipos ](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** ou **nvarchar(max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **ntext**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caractere Unicode, em seguida, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client inspeciona o DBCOLUMNDESC *rgPropertySets*membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **nchar**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client mapeia o tipo para **nvarchar**. Em ambos os casos, o membro *ulColumnSize* de DBCOLUMNDESC determina a largura da coluna do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Ao criar uma nova tabela, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeia apenas os valores de enumeração do tipo de dados OLE DB especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
