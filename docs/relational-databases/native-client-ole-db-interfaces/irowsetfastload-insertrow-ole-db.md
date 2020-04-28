---
title: IRowsetFastLoad::InsertRow (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c178f2e948e27b964b04f62508ec35038b204576
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307260"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Adiciona uma linha ao conjunto de linhas de cópia em massa. Para obter exemplos, confira [Copiar Dados em massa usando IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) e [Enviar dados de blob para o SQL Server usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 SQLNCLI11 não pôde alocar memória suficiente para concluir a solicitação.  
  
 E_UNEXPECTED  
 O método foi chamado em um conjunto de linhas de cópia em massa invalidado anteriormente pelo método [IRowsetFastLoad::Commit](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md).  
  
 DB_E_BADACCESSORHANDLE  
 O argumento *hAccessor* fornecido pelo consumidor era inválido.  
  
 DB_E_BADACCESSORTYPE  
 O acessador especificado não era um acessador de linha ou não especificou a memória de propriedade do consumidor.  
  
## <a name="remarks"></a>Comentários  
 Um erro ao converter dados do consumidor no tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma coluna gera um retorno E_FAIL do provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Os dados podem ser transmitidos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em qualquer método **InsertRow** ou apenas no método **Commit**. O aplicativo do consumidor pode chamar o método **InsertRow** muitas vezes com dados incorretos antes ser avisado de que há um erro de conversão de tipo de dados. Como o método **Commit** assegura que todos os dados sejam especificados corretamente pelo consumidor, ele pode usar o método **Commit** apropriadamente para validar os dados, conforme necessário.  
  
 Os conjuntos de linhas de cópia em massa do provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client são somente gravação. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não expõe nenhum método que permite consultas do consumidor do conjunto de linhas. Para encerrar o processamento, o consumidor pode liberar sua referência na interface [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) sem chamar o método **Commit**. Não há nenhum recurso para acessar uma linha inserida pelo consumidor no conjunto de linhas e alterar seus valores ou para removê-la individualmente do conjunto de linhas.  
  
 As linhas copiadas em massa são formatadas no servidor para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O formato de linha é afetado por todas as opções que possam ter sido definidas para a conexão ou sessão, como ANSI_PADDING. Essa opção é ativada por padrão para qualquer conexão feita por meio do provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="see-also"></a>Consulte Também  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
