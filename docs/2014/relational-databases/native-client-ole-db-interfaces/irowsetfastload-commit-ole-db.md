---
title: 'IRowsetFastLoad:: Commit (OLE DB) | Microsoft Docs'
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
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 553f3aaaceae23944ae9b2d0be7d8129a22c0dd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019804"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  Marca o término de um lote de linhas inseridas e escreve as linhas na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter exemplos, consulte [em massa dados usando IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md) e [enviar dados BLOB ao SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de linhas de cópia em massa Native Client OLE DB provider se comporta como um conjunto de linhas do modo de atualização com atraso. Como o usuário insere dados de linha no conjunto de linhas, linhas inseridas são tratadas da mesma forma como inserções pendentes em um conjunto de linhas com suporte **IRowsetUpdate**.  
  
 O consumidor deve chamar o **confirmar** método no conjunto de linhas de cópia em massa para gravar as linhas inseridas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela da mesma maneira como o **IRowsetUpdate:: Update** método é usado para enviar linhas pendentes para um instância do SQL Server.  
  
 Se o consumidor libere a referência no conjunto de linhas de cópia em massa sem chamar o **confirmar** método, inserido todas as linhas não gravadas previamente são perdidas.  
  
 O consumidor pode processar em lotes linhas inseridas chamando o **confirmar** método com o *fDone* argumento definido como FALSE. Quando *fDone*é definida como TRUE, o conjunto de linhas se torna inválido. Um conjunto de linhas de cópia em massa inválido oferece suporte apenas a **ISupportErrorInfo** interface e **IRowsetFastLoad:: Release** método.  
  
## <a name="see-also"></a>Consulte também  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  