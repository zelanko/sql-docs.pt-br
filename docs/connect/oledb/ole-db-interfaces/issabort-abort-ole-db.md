---
title: ISSAbort::Abort (Driver do OLE DB) | Microsoft Docs
description: Saiba como o método ISSAbort::Abort cancela o conjunto de linhas atual e todos os comandos em lote associados ao comando atual no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18e8c8544c557292bd5a7cc813d809ea0f9cf061
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860074"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cancela o conjunto de linhas atual, além de todos os comandos em lote associados ao comando atual.  
  
A interface `ISSAbort`, que é exposta no OLE DB Driver for SQL Server, fornece o método `ISSAbort::Abort` que é usado para cancelar o conjunto de linhas atual, além de todos os comandos executados em lotes com o comando que gerou inicialmente o conjunto de linhas e cuja execução ainda não foi concluída.  
  
 `ISSAbort` é uma interface específica do OLE DB Driver for SQL Server disponível por meio do uso de `QueryInterface` no objeto `IMultipleResults` retornado por `ICommand::Execute` ou `IOpenRowset::OpenRowset`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Comentários  
 Se o comando que está sendo anulado estiver em um procedimento armazenado, a execução dele (e de outros procedimentos que chamaram esse procedimento) será encerrada, bem como o lote de comandos que contém a chamada de procedimento armazenado. Se o servidor estiver no processo de transferir um conjunto de resultados para o cliente, a transferência será interrompida. Se o cliente não quiser consumir um conjunto de resultados, `**`ISSAbort::Abort` before releasing the rowset will speed up the rowset release, but if there is an open transaction and XACT_ABORT is ON, the transaction will be rolled back when ` será chamado  
  
 Depois que `ISSAbort::Abort` retorna S_OK, a interface `IMultipleResults` associada entra em um estado inutilizável e retorna DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface `IUnknown`) até que seja liberada. Se um `IRowset` foi obtido de `IMultipleResults` antes de uma chamada para `Abort`, também entrará em um estado inutilizável e retornará DB_E_CANCELED para todas as chamadas de método (com exceção dos métodos definidos pela interface `IUnknown` e `IRowset::ReleaseRows`) até que seja liberado após uma chamada bem-sucedida para `ISSAbort::Abort`.  
  
> [!NOTE]  
>  Do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] em diante, se o estado XACT_ABORT do servidor for ON, a execução de `ISSAbort::Abort` será encerrada e reverterá qualquer transação implícita ou explícita atual quando conectada ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não anularão a transação atual.  
  
## <a name="arguments"></a>Argumentos  
 Nenhum.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método `ISSAbort::Abort` retorna S_OK se o lote foi cancelado e DB_E_CANTCANCEL em caso contrário. Se o lote já foi cancelado, DB_E_CANCELED será retornado.  
  
 DB_E_CANCELED  
 O lote já foi cancelado.  
  
 DB_E_CANTCANCEL  
 O lote não foi cancelado.  
  
 E_FAIL  
 Um erro específico do provedor ocorreu. Para obter informações detalhadas, use a interface [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15).  
  
 E_UNEXPECTED  
 A chamada para o método era inesperada. Por exemplo, o objeto está em um estado de zumbi porque `ISSAbort::Abort` já foi chamado.  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
  
