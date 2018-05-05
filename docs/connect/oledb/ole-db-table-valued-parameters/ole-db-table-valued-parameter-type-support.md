---
title: Suporte ao tipo de parâmetro com valor de tabela de banco de dados OLE | Microsoft Docs
description: Suporte para tipo de parâmetro de DB Table-Valued OLE
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8f1a20a09e4c15b0dbe84352a4bfbbef59b5d784
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Suporte ao tipo de parâmetro com valor de tabela OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artigo descreve o suporte de tipo de OLE DB para parâmetros com valor de tabela.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de linhas de parâmetro com valor de tabela  
 É possível criar um objeto de conjunto de linhas especializado para parâmetros com valor de tabela. Você pode criar o objeto de conjunto de linhas de parâmetro com valor de tabela usando ITableDefinitionWithConstraints::CreateTableWithConstraints ou IOpenRowset:: OPENROWSET. Para fazer isso, defina o *eKind* membro o *pTableID* parâmetro como DBKIND_GUID_NAME e forneça o CLSID_ROWSET_INMEMORY como o *guid* membro. O nome do tipo de servidor para o parâmetro com valor de tabela deve ser especificado no *pwszName* membro *pTableID* ao usar IOpenRowset:: OPENROWSET. O objeto de conjunto de linhas de parâmetro com valor de tabela se comporta como um regular OLE DB Driver para o objeto do SQL Server.  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 Um tipo novo, DBTYPE_TABLE, representa um tipo de tabela. Esse tipo especifica parâmetros com valor de tabela em várias interfaces OLE DB em que um DBTYPE é obrigatório.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE tem o mesmo formato de DBTYPE_IUNKNOWN. É um ponteiro para um objeto no buffer de dados. Para obter a especificação completa nas associações, o consumidor preenche o buffer DBOBJECT, com *iid* definido como uma das interfaces de objeto de conjunto de linhas (IID_IRowset). Se nenhum DBOBJECT for especificado nas associações, IID_IRowset será assumido.  
  
 Não há suporte para conversões para e de DBTYPE_TABLE para qualquer outro tipo. IConvertType::CanConvert retornará S_FALSE em conversão sem suporte para qualquer solicitação que não seja a conversão de DBTYPE_TABLE para. Isso supõe DBCONVERTFLAGS_PARAMETER no objeto de comando.  
  
## <a name="methods"></a>Métodos  
 Para obter informações sobre métodos OLE DB que oferecem suporte a parâmetros com valor de tabela, consulte [suporte de tipo de parâmetro OLE DB Table-Valued &#40;métodos&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propriedades  
 Para obter informações sobre propriedades de OLE DB que oferecem suporte a parâmetros com valor de tabela, consulte [suporte de tipo de parâmetro OLE DB Table-Valued &#40;propriedades&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar com valor de tabela parâmetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
