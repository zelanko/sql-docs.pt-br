---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAbort::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0729183a2e5be91d3cdb30eae3ae5990f8398103
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115422"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
  Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 Se o comando que está sendo anulado está em um procedimento armazenado, a execução deste (e de quaisquer procedimentos armazenados que chamaram esse procedimento) será encerrada, bem como o lote de comandos que contém a chamada de procedimento armazenado. Se o servidor estiver no processo de transferir um conjunto de resultados para o cliente, ele será interrompido. Se o cliente não desejar consumir um conjunto de resultados, chamar **ISSAbort::Abort** antes de liberar o conjunto de linhas agilizará a liberação do conjunto de resultados, mas se houver uma transação aberta e XACT_ABORT estiver ON, a transação será revertida quando **ISSAbort::Abort** for chamado.  
  
 Depois que **ISSAbort::Abort** retornar S_OK, a interface **IMultipleResults** associada entrará em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface **IUnknown** ) até que seja liberada. Se um **IRowset** foi obtido de **IMultipleResults** antes de uma chamada para **Abort**, também entrará em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface **IUnknown** e **IRowset::ReleaseRows**) até que seja liberado após uma chamada bem-sucedida para **ISSAbort::Abort**.  
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se o estado XACT_ABORT do servidor está ativada, executando **issabort:: Abort** encerrará e reverter qualquer implícita ou explícita transação atual quando conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não anularão a transação atual.  
  
## <a name="arguments"></a>Argumentos  
 Nenhum.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método **ISSAbort::Abort** retorna S_OK se o lote foi cancelado e DB_E_CANTCANCEL em caso contrário. Se o lote já foi cancelado, DB_E_CANCELED será retornado.  
  
 DB_E_CANCELED  
 O lote já foi cancelado.  
  
 DB_E_CANTCANCEL  
 O lote não foi cancelado.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor; Para obter informações detalhadas, use o [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) interface.  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o objeto está em um estado de zumbi porque **ISSAbort::Abort** já foi chamado.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
## <a name="see-also"></a>Consulte também  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  