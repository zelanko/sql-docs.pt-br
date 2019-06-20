---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 142f6ac339e437877c485588333fabb04e0bd66b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241345"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
  A interface **IBCPSession** expõe o suporte a operações de cópia em massa baseada em arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A interface **IBCPSession** é exposta no provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no mesmo nível que Sessões. No provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, os objetos de fonte de dados são fábricas de objetos de sessão e as operações de cópia em massa são especificadas na propriedade de conexão SSPROP_ENABLEBULKCOPY. Além disso, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como verdadeira.  
  
 Chamar o método **IDBCreateSession::CreateSession** resultará na criação de um objeto **BulkCopySession** . Todos os métodos de cópia em massa com base em arquivo expostos pelo objeto **IBCPSession** poderão, então, ser chamados com assinaturas semelhantes na interface **IBCPSession** desse objeto **IBCPSession** .  
  
> [!NOTE]  
>  O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte a operações de cópia em massa com base em memória por meio da interface [IRowsetFastLoad](irowsetfastload-ole-db.md) .  
  
 Para obter mais informações sobre como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client para operações de cópia em massa, consulte [executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md).  
  
 Para obter um exemplo que mostra como usar o **IBCPSession** interface, consulte [IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Descrição|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|Cria uma associação entre variáveis de programa e colunas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Ibcpsession:: BCPColumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|Define as opções para uma operação de cópia em massa.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|Confirma as linhas restantes a serem enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPExec &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|Executa a operação de cópia em massa.|  
|[Ibcpsession:: BCPInit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|Inicializa a estrutura de cópia em massa, executa alguma verificação de erros, verifica se os nomes dos arquivos de formato e de dados estão corretos e, então, os abre.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|Lê informações de formato relativas a cada coluna no arquivo de formato.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|Grava informações de formato relativas a cada coluna no arquivo de formato.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
