---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7ccd40edb997ae3e45fd705a8a6543c8f3895b6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119507"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
  O **IBCPSession** interface expõe o suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operações de cópia em massa baseadas em arquivo. O **IBCPSession** interface é exposta no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB Native Client no mesmo nível que sessões. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client, objetos de fonte de dados são fábricas de objetos de sessão e operações de cópia em massa são especificadas na propriedade conexão SSPROP_ENABLEBULKCOPY. Além disso, a propriedade SSPROP_ENABLEFASTLOAD deve ser definida como verdadeira.  
  
 Chamar o método **IDBCreateSession::CreateSession** resultará na criação de um objeto **BulkCopySession** . Todos os métodos de cópia em massa com base em arquivo expostos pelo objeto **IBCPSession** poderão, então, ser chamados com assinaturas semelhantes na interface **IBCPSession** desse objeto **IBCPSession** .  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte a operações de cópia em massa baseadas em memória por meio de [IRowsetFastLoad](irowsetfastload-ole-db.md) interface.  
  
 Para obter mais informações sobre como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider para operações de cópia em massa, consulte [executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md).  
  
 Para obter um exemplo mostrando como usar o **IBCPSession** interface, consulte [IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Método|Description|  
|------------|-----------------|  
|[Ibcpsession:: BCPColFmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|Cria uma associação entre variáveis de programa e colunas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPColumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|Define o número de campos que devem ser associados às colunas de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|Define as opções para uma operação de cópia em massa.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|Confirma as linhas restantes a serem enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Ibcpsession:: BCPExec &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|Executa a operação de cópia em massa.|  
|[Ibcpsession:: BCPInit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|Inicializa a estrutura de cópia em massa, executa alguma verificação de erros, verifica se os nomes dos arquivos de formato e de dados estão corretos e, então, os abre.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|Lê informações de formato relativas a cada coluna no arquivo de formato.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|Grava informações de formato relativas a cada coluna no arquivo de formato.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  