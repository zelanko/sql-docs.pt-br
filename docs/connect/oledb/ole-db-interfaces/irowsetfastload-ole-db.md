---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
description: IRowsetFastLoad (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: eea2e77e5280044a8bb17a0eca33ed68da0c054d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O **IRowsetFastLoad** interface expõe o suporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operações de cópia em massa com base em memória. Driver do OLE DB para SQL Server usam a interface para rapidamente adicionar dados a um existente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela.  
  
 Se você definir SSPROP_ENABLEFASTLOAD como VARIANT_TRUE para uma sessão, não poderá ler dados de conjuntos de linhas subsequentemente passados como retorno dessa sessão. Quando SSPROP_ENABLEFASTLOAD é definido como VARIANT_TRUE, todos os conjuntos de linhas criados na sessão serão do tipo IRowsetFastLoad. Conjuntos de linhas iRowsetFastLoad não oferecem suporte a funcionalidade de busca do conjunto de linhas; Portanto, não não possível ler dados desses conjuntos de linhas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Description|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[IRowsetFastLoad:: Insertrow &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Adiciona uma linha ao conjunto de linhas de cópia em massa.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [Usando IRowsetFastLoad de dados de cópia em massa &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar dados BLOB ao SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM & #40; OLE DB & #41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
