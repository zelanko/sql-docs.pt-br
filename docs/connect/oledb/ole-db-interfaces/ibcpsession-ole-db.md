---
title: IBCPSession (OLE DB) | Microsoft Docs
description: Interface IBCPSession (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 6fc35b0e8d964d07987263fa05e2647da6fefdd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790768"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A interface **IBCPSession** expõe o suporte a operações de cópia em massa baseada em arquivo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O **IBCPSession** interface é exposta no Driver do OLE DB para SQL Server no mesmo nível que sessões. No OLE DB Driver for SQL Server, os objetos de fonte de dados são fábricas de objetos de Sessão e as operações de cópia em massa são especificadas na propriedade de conexão SSPROP_ENABLEBULKCOPY. Além disso, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como verdadeira.  
  
 Chamar o método **IDBCreateSession::CreateSession** resultará na criação de um objeto **BulkCopySession** . Todos os métodos de cópia em massa com base em arquivo expostos pelo objeto **IBCPSession** poderão, então, ser chamados com assinaturas semelhantes na interface **IBCPSession** desse objeto **IBCPSession** .  
  
> [!NOTE]  
>  O OLE DB Driver for SQL Server dá suporte a operações de cópia em massa baseadas em memória por meio da interface [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md).  
  
 Para obter mais informações sobre como usar o Driver do OLE DB para SQL Server para operações de cópia em massa, consulte [executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md).  
  
 Para obter um exemplo que mostra como usar o **IBCPSession** interface, consulte [IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Descrição|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Cria uma associação entre variáveis de programa e colunas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[Ibcpsession:: BCPColumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Define as opções para uma operação de cópia em massa.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Confirma as linhas restantes a serem enviadas ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPExec &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Executa a operação de cópia em massa.|  
|[Ibcpsession:: BCPInit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Inicializa a estrutura de cópia em massa, executa alguma verificação de erros, verifica se os nomes dos arquivos de formato e de dados estão corretos e, então, os abre.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Lê informações de formato relativas a cada coluna no arquivo de formato.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Grava informações de formato relativas a cada coluna no arquivo de formato.|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
