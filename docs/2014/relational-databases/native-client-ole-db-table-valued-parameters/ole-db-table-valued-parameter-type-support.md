---
title: Suporte ao tipo de parâmetro com valor de tabela do OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ea078b34dee99b3bc2b97f6c0ce2a6ee8d25113
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018122"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Suporte ao tipo de parâmetro com valor de tabela OLE DB
  Este tópico descreve suporte ao tipo OLE DB para parâmetros com valor de tabela.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de linhas de parâmetro com valor de tabela  
 É possível criar um objeto de conjunto de linhas especializado para parâmetros com valor de tabela. Você cria o objeto de conjunto de linhas de parâmetro com valor de tabela usando ITableDefinitionWithConstraints::CreateTableWithConstraints ou IOpenRowset::OpenRowset. Para fazer isso, defina o membro *eKind* do parâmetro *pTableID* como DBKIND_GUID_NAME e forneça o CLSID_ROWSET_INMEMORY como o membro *guid*. O nome do tipo de servidor para parâmetro com valor de tabela deve ser especificado no membro *pwszName* de *pTableID* ao usar IOpenRowset::OpenRowset. O objeto de conjunto de linhas para parâmetros com valor de tabela se comporta como um objeto do provedor OLE DB do SQL Server Native Client normal.  
  
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
  
## <a name="dbtype_table"></a>DBTYPE_TABLE  
 Um tipo novo, DBTYPE_TABLE, representa um tipo de tabela. Esse tipo especifica parâmetros com valor de tabela em várias interfaces OLE DB em que um DBTYPE é obrigatório.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE tem o mesmo formato de DBTYPE_IUNKNOWN. Trata-se de um ponteiro para um objeto no buffer de dados. Para obter a especificação completa nas associações, o consumidor preenche o buffer DBOBJECT, com *iid* definido como uma das interfaces de objeto de conjunto de linhas (IID_IRowset). Se nenhum DBOBJECT for especificado nas associações, IID_IRowset será assumido.  
  
 Não há suporte para conversões para e de DBTYPE_TABLE para qualquer outro tipo. IConvertType::CanConvert retornará S_FALSE em uma conversão não compatível para qualquer solicitação que não seja a conversão de DBTYPE_TABLE em DBTYPE_TABLE. Isso supõe DBCONVERTFLAGS_PARAMETER no objeto Command.  
  
## <a name="methods"></a>Métodos  
 Para obter informações sobre métodos do OLE DB que dão suporte a parâmetros com valor de tabela, confira [Suporte ao tipo de parâmetro com valor de tabela OLE DB &#40;Métodos&#41;](ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propriedades  
 Para obter informações sobre propriedades do OLE DB que dão suporte a parâmetros com valor de tabela, confira [Suporte ao tipo de parâmetro com valor de tabela OLE DB &#40;Propriedades&#41;](ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Os parâmetros com valor de tabela &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
