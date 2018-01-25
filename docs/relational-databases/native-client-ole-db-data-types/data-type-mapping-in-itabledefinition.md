---
title: Mapeamento de tipo de dados em ITableDefinition | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6e67b2b12d10053478013d737df7120c2047f60
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>Mapeamento do tipo de dados em ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao criar tabelas usando o **itabledefinition:: CreateTable** função, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client pode especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados no *pwszTypeName* membro da matriz DBCOLUMNDESC passada. Se o consumidor Especifica o tipo de dados de uma coluna por nome, de tipo de dados OLE DB mapeamento, representado pelo *wType* membro da estrutura DBCOLUMNDESC, é ignorado.  
  
 Ao especificar novos tipos de dados de coluna com tipos de dados de OLE DB usando a estrutura DBCOLUMNDESC *wType* membro, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia tipos de dados OLE DB da seguinte maneira.  
  
|Tipo de dados OLE DB|SQL Server<br /><br /> tipo de dados|Informações adicionais|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binário**, **varbinary**, **imagem,** ou **varbinary (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor e na versão da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **imagem**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de um **binário** coluna de tipo de dados, em seguida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona o membro *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **binário**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **varbinary**. Em ambos os casos, o membro *ulColumnSize* membro determina a largura da coluna do SQL Server criada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona os MEMBROS *bPrecision* e *bScale* membros para determinar a precisão e escala para o **numérico** coluna.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **texto,** ou **varchar (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor de versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **texto**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caracteres multibyte, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona o membro *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **char**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **varchar**. Em ambos os casos, o membro *ulColumnSize* membro determina a largura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna criada.|  
|DBTYPE_UDT|**UDT**|As informações a seguir são usadas em **DBCOLUMNDESC** estruturas por **itabledefinition:: CreateTable** quando colunas UDT são necessárias:<br /><br /> *pwSzTypeName* is ignored.<br /><br /> *rgPropertySets* deve incluir um **DBPROPSET_SQLSERVERCOLUMN** propriedade definida conforme descrito na seção sobre **DBPROPSET_SQLSERVERCOLUMN**, na [definida pelo usuário usando o Tipos de](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** ou **nvarchar (max)**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona o *ulColumnSize* membro da estrutura DBCOLUMNDESC. Com base no valor, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **ntext**.<br /><br /> Se o valor de *ulColumnSize* é menor do que o comprimento máximo de uma coluna de tipo de dados de caractere Unicode, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client inspeciona o membro *rgPropertySets* membro. Caso DBPROP_COL_FIXEDLENGTH seja VARIANT_TRUE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **nchar**. Se o valor da propriedade seja VARIANT_FALSE, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client mapeia o tipo para **nvarchar**. Em ambos os casos, o membro *ulColumnSize* membro determina a largura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coluna criada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Ao criar uma nova tabela, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeia apenas os valores de enumeração do tipo de dados OLE DB especificados na tabela anterior. Tentar criar uma tabela com uma coluna de qualquer outro tipo de dados OLE DB gera um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
