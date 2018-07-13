---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 745282c1d1e8fa36c9d0a407ac32171304d05197
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417165"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter exemplos, consulte [em massa dados usando IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md) e [enviar dados de BLOB para SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;do OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Commit(  
BOOL   
fDone  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *fDone*[in]  
 Se FALSE, o conjunto de linhas manterá validade e poderá ser usado pelo consumidor para inserção de linha adicional. Caso seja TRUE, o conjunto de linhas perde validade e nenhuma inserção adicional pode ser feita pelo consumidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método teve êxito e todos os dados inseridos foram escritos na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Ocorreu um erro específico de provedor. Recupere informações de erro para o texto de erro específico do provedor.  
  
 E_UNEXPECTED  
 O método foi chamado em um conjunto de linhas de cópia em massa invalidado anteriormente pelo **IRowsetFastLoad:: Commit** método.  
  
## <a name="remarks"></a>Remarks  
 Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de linhas cópia em massa de provedor de OLE DB do Native Client se comporta como um conjunto de linhas do modo de atualização com atraso. Como o usuário insere dados de linha no conjunto de linhas, as linhas inseridas são tratadas da mesma forma como inserções pendentes em um conjunto de linhas que dão suporte a **IRowsetUpdate**.  
  
 O consumidor deve chamar o **confirmar** método no conjunto de linhas de cópia em massa para gravar as linhas inseridas as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela da mesma maneira como o **IRowsetUpdate:: Update** método é usado para enviar linhas pendentes para um instância do SQL Server.  
  
 Se o consumidor libera sua referência no conjunto de linhas de cópia em massa sem chamar o **confirmar** método, inserido todas as linhas não gravadas previamente são perdidas.  
  
 O consumidor pode criar lotes de linhas inseridas por meio da chamada a **Commit** método com o *fDone* argumento definido como FALSE. Quando *fDone*é definido como TRUE, o conjunto de linhas se torna inválido. Um conjunto de linhas de cópia em massa inválido oferece suporte apenas a **ISupportErrorInfo** interface e **IRowsetFastLoad::Release** método.  
  
## <a name="see-also"></a>Consulte também  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
