---
title: IRowsetFastLoad (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c38cd2ea900da079ffe6e9aac75ce967abc4ffee
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243917"
---
# <a name="irowsetfastload-native-client-ole-db-provider"></a>IRowsetFastLoad (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Uma interface **IRowsetFastLoad** expõe o suporte para operações de cópia em massa baseadas em memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Os consumidores do provedor de OLE DB de cliente nativo usam a interface para adicionar dados rapidamente a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela existente.  
  
 Se você definir SSPROP_ENABLEFASTLOAD como VARIANT_TRUE para uma sessão, não poderá ler dados de conjuntos de linhas subsequentemente passados como retorno dessa sessão. Quando SSPROP_ENABLEFASTLOAD for definido como VARIANT_TRUE, todos os conjuntos de linhas criados na sessão serão do tipo IRowsetFastLoad. Os conjuntos de linhas IRowsetFastLoad não dão suporte à funcionalidade de fetch de conjuntos de linhas; portanto, os dados desses conjuntos de linhas não podem ser lidos.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Descrição|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Adiciona uma linha ao conjunto de linhas de cópia em massa.|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Copiar Dados em massa usando o IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar dados BLOB ao SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
