---
title: IRowsetFastLoad::InsertRow (OLE DB) | Microsoft Docs
description: IRowsetFastLoad::InsertRow (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b01c63e74ee26cea327a01e3bf9a3595bc5012d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015453"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Adiciona uma linha ao conjunto de linhas de cópia em massa. Para obter exemplos, consulte [copiar dados em massa &#40;usando&#41; o IRowsetFastLoad OLE DB](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) e [enviar dados de BLOB para o SQL &#40;Server&#41;usando o IRowsetFastLoad e o ISEQUENTIALSTREAM OLE DB](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hAccessor*[in]  
 O identificador do acessador que define os dados de linha para cópia em massa. O acessador referenciado é um acessador de linha, que associa a memória de propriedade do consumidor contendo valores de dados.  
  
 *pData*[in]  
 Um ponteiro para a memória de propriedade do consumidor que contém valores de dados. Para obter mais informações, consulte [Estruturas DBBINDING](https://go.microsoft.com/fwlink/?LinkId=65955).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido. Todos os valores de status associados para todas as colunas têm o valor DBSTATUS_S_OK ou DBSTATUS_S_NULL.  
  
 E_FAIL  
 Ocorreu um erro. As informações do erro estão disponíveis nas interfaces de erro do conjunto de linhas.  
  
 E_INVALIDARG  
 O argumento *pData* foi definido como um ponteiro NULL.  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL não pôde alocar memória suficiente para concluir a solicitação.  
  
 E_UNEXPECTED  
 O método foi chamado em um conjunto de linhas de cópia em massa invalidado anteriormente pelo método [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) .  
  
 DB_E_BADACCESSORHANDLE  
 O argumento *hAccessor* fornecido pelo consumidor era inválido.  
  
 DB_E_BADACCESSORTYPE  
 O acessador especificado não era um acessador de linha ou não especificou a memória de propriedade do consumidor.  
  
## <a name="remarks"></a>Remarks  
 Um erro ao converter dados do consumidor no tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma coluna gera um retorno E_FAIL do OLE DB Driver for SQL Server. Os dados podem ser transmitidos para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em qualquer método **InsertRow** ou apenas no método **Commit**. O aplicativo do consumidor pode chamar o método **InsertRow** muitas vezes com dados incorretos antes ser avisado de que há um erro de conversão de tipo de dados. Como o método **Commit** assegura que todos os dados sejam especificados corretamente pelo consumidor, ele pode usar o método **Commit** apropriadamente para validar os dados, conforme necessário.  
  
 O driver de OLE DB para conjuntos de linhas de cópia em massa do SQL Server são somente gravação. O driver OLE DB para SQL Server não expõe nenhum método que permita a consulta de consumidor do conjunto de linhas. Para encerrar o processamento, o consumidor pode liberar sua referência na interface [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) sem chamar o método **Commit**. Não há nenhum recurso para acessar uma linha inserida pelo consumidor no conjunto de linhas e alterar seus valores ou para removê-la individualmente do conjunto de linhas.  
  
 As linhas copiadas em massa são formatadas no servidor para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O formato de linha é afetado por todas as opções que possam ter sido definidas para a conexão ou sessão, como ANSI_PADDING. Essa opção é definida por padrão para qualquer conexão feita por meio do driver OLE DB para SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [OLE DB &#40;IRowsetFastLoad&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
