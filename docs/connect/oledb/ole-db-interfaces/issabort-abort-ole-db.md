---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
description: ISSAbort::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0c7d30e8132d245958e7ef6f7f09e642a2da960c
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305375"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.  
  
O **ISSAbort** interface, que é exposta no Driver OLE DB para SQL Server, oferece o **issabort:: Abort** método que é usado para cancelar o conjunto de linhas atual, além de todos os comandos em lotes com o comando que gerou inicialmente o conjunto de linhas, e que ainda não concluiu a execução.  
  
 **ISSAbort** é um Driver OLE DB para a interface específicas do SQL Server disponíveis usando **QueryInterface** no **IMultipleResults** objeto retornado por **ICommand:: execute**  ou **IOpenRowset:: OPENROWSET**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 Se o comando que está sendo anulado está em um procedimento armazenado, a execução do procedimento armazenado (e quaisquer procedimentos que chamaram esse procedimento) será encerrada, bem como o lote de comando que contém a chamada de procedimento armazenado. Se o servidor está no processo de transferência de um conjunto de resultados para o cliente, a transferência será interrompida. Se o cliente não desejar consumir um conjunto de resultados, chamar **ISSAbort::Abort** antes de liberar o conjunto de linhas agilizará a liberação do conjunto de resultados, mas se houver uma transação aberta e XACT_ABORT estiver ON, a transação será revertida quando **ISSAbort::Abort** for chamado.  
  
 Depois de **issabort:: Abort** Retorna S_OK, associado **IMultipleResults** interface entra em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (exceto os métodos definidos pelo **IUnknown** interface) até que ele seja liberado. Se um **IRowset** foi obtido de **IMultipleResults** antes de uma chamada para **Abort**, também entrará em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface **IUnknown** e **IRowset::ReleaseRows**) até que seja liberado após uma chamada bem-sucedida para **ISSAbort::Abort**.  
  
> [!NOTE]  
>  Começando com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se o estado XACT_ABORT do servidor está ativada, executando **issabort:: Abort** encerrará e reverter qualquer implícita ou explícita transação atual quando conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não anularão a transação atual.  
  
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
 Ocorreu um erro específico do provedor; Para obter informações detalhadas, use o [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interface.  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o objeto está em um estado de zumbi porque **ISSAbort::Abort** já foi chamado.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
  
