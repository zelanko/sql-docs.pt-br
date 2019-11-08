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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f3ea8d1e52ba5fc4d34f5bee1c728ff7ca3db2d7
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789581"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A interface **IBCPSession** oferece suporte para operações de cópia em massa com base em arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A interface **IBCPSession** é exposta no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no mesmo nível que Sessões. No provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, os objetos de fonte de dados são fábricas de objetos de sessão e as operações de cópia em massa são especificadas na propriedade de conexão SSPROP_ENABLEBULKCOPY. Além disso, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como verdadeira.  
  
 Chamar o método **IDBCreateSession::CreateSession** resultará na criação de um objeto **BulkCopySession** . Todos os métodos de cópia em massa com base em arquivo expostos pelo objeto **IBCPSession** poderão, então, ser chamados com assinaturas semelhantes na interface **IBCPSession** desse objeto **IBCPSession** .  
  
> [!NOTE]  
>  O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte a operações de cópia em massa com base em memória por meio da interface [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) .  
  
 Para obter mais informações sobre como usar o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para operações de cópia em massa, consulte [executando operações de cópia em massa](../../relational-databases/native-client/features/performing-bulk-copy-operations.md).  
  
 Para obter um exemplo que mostra como usar a interface **IBCPSession** , consulte [IBCPSession:: &#40;BCPDone&#41;OLE DB](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Descrição|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Cria uma associação entre variáveis de programa e colunas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[IBCPSession:: BCPColumns &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[IBCPSession:: BCPControl &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Define as opções para uma operação de cópia em massa.|  
|[IBCPSession:: BCPDone &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Confirma as linhas restantes a serem enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[IBCPSession:: BCPExec &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Executa a operação de cópia em massa.|  
|[IBCPSession:: BCPInit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Inicializa a estrutura de cópia em massa, executa alguma verificação de erros, verifica se os nomes dos arquivos de formato e de dados estão corretos e, então, os abre.|  
|[IBCPSession:: BCPReadFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Lê informações de formato relativas a cada coluna no arquivo de formato.|  
|[IBCPSession:: BCPWriteFmt &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Grava informações de formato relativas a cada coluna no arquivo de formato.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
