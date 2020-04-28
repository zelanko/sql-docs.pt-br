---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 653bd8aad3a10a3929b7ced76e28e4d570733ad3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307337"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A interface **IBCPSession** expõe o suporte a operações de cópia em massa baseada em arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A interface **IBCPSession** é exposta no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no mesmo nível que Sessões. No provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, os objetos de fonte de dados são fábricas de objetos de sessão e as operações de cópia em massa são especificadas na propriedade de conexão SSPROP_ENABLEBULKCOPY. Além disso, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como verdadeira.  
  
 Chamar o método **IDBCreateSession::CreateSession** resultará na criação de um objeto **BulkCopySession** . Todos os métodos de cópia em massa com base em arquivo expostos pelo objeto **IBCPSession** poderão, então, ser chamados com assinaturas semelhantes na interface **IBCPSession** desse objeto **IBCPSession** .  
  
> [!NOTE]  
>  O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte a operações de cópia em massa com base em memória por meio da interface [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) .  
  
 Para obter mais informações sobre como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar o provedor de OLE DB de cliente nativo para operações de cópia em massa, consulte [executando operações de cópia em massa](../../relational-databases/native-client/features/performing-bulk-copy-operations.md).  
  
 Para obter um exemplo de como usar a interface **IBCPSession**, confira [IBCPSession::BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Descrição|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Cria uma associação entre variáveis de programa e colunas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[IBCPSession::BCPColumns &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[IBCPSession::BCPControl &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Define as opções para uma operação de cópia em massa.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Confirma as linhas restantes a serem enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[IBCPSession::BCPExec &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Executa a operação de cópia em massa.|  
|[IBCPSession::BCPInit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Inicializa a estrutura de cópia em massa, executa alguma verificação de erros, verifica se os nomes dos arquivos de formato e de dados estão corretos e, então, os abre.|  
|[IBCPSession::BCPReadFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Lê informações de formato relativas a cada coluna no arquivo de formato.|  
|[IBCPSession::BCPWriteFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Grava informações de formato relativas a cada coluna no arquivo de formato.|  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
