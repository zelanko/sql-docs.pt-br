---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29ab30077814e79d19df00776d6bdfa65739f2a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639905"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.  
  
O **ISSAbort** interface, que é exposta na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client, fornece o **issabort:: Abort** método que é usado para cancelar o conjunto de linhas atual, além de todos os comandos em lote com o comando que gerou inicialmente o conjunto de linhas, e que ainda não concluiu a execução.  
  
 **ISSAbort** é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interface específica do provedor de Native Client disponível por meio **QueryInterface** sobre o **IMultipleResults** objeto retornado por  **ICommand:: execute** ou **IOpenRowset:: OPENROWSET**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Comentários  
 Se o comando que está sendo anulado está em um procedimento armazenado, a execução deste (e de quaisquer procedimentos armazenados que chamaram esse procedimento) será encerrada, bem como o lote de comandos que contém a chamada de procedimento armazenado. Se o servidor estiver no processo de transferir um conjunto de resultados para o cliente, ele será interrompido. Se o cliente não desejar consumir um conjunto de resultados, chamar **ISSAbort::Abort** antes de liberar o conjunto de linhas agilizará a liberação do conjunto de resultados, mas se houver uma transação aberta e XACT_ABORT estiver ON, a transação será revertida quando **ISSAbort::Abort** for chamado.  
  
 Depois que **ISSAbort::Abort** retornar S_OK, a interface **IMultipleResults** associada entrará em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface **IUnknown** ) até que seja liberada. Se um **IRowset** foi obtido de **IMultipleResults** antes de uma chamada para **Abort**, também entrará em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface **IUnknown** e **IRowset::ReleaseRows**) até que seja liberado após uma chamada bem-sucedida para **ISSAbort::Abort**.  
  
> [!NOTE]  
>  Do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] em diante, se o estado XACT_ABORT do servidor for ON, a execução de **ISSAbort::Abort** será encerrada e reverterá qualquer transação implícita ou explícita atual quando conectada ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não anularão a transação atual.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [ISSAbort &#40;OLE DB&#41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
