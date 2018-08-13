---
title: 'IRowsetFastLoad:: Insertrow (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
ms.assetid: 594d3461-34d2-41e7-8ad4-bd2753601ab6
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 404068023a2a62739286134f8fda08184e4844c8
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562510"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Adiciona uma linha ao conjunto de linhas de cópia em massa. Para obter exemplos, consulte [em massa dados usando IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) e [enviar dados de BLOB para SQL SERVER usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;do OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
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
 Um ponteiro para a memória de propriedade do consumidor que contém valores de dados. Para obter mais informações, consulte [Estruturas DBBINDING](http://go.microsoft.com/fwlink/?LinkId=65955).  
  
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
  
## <a name="remarks"></a>Remarks  
 Um erro ao converter dados do consumidor para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados para uma coluna gera um retorno de E_FAIL o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client. Os dados podem ser transmitidos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em qualquer método **InsertRow** ou apenas no método **Commit**. O aplicativo do consumidor pode chamar o método **InsertRow** muitas vezes com dados incorretos antes ser avisado de que há um erro de conversão de tipo de dados. Como o método **Commit** assegura que todos os dados sejam especificados corretamente pelo consumidor, ele pode usar o método **Commit** apropriadamente para validar os dados, conforme necessário.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas cópia em massa de provedor de OLE DB do Native Client são somente gravação. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client não expõe nenhum método que permite consultas do consumidor do conjunto de linhas. Para encerrar o processamento, o consumidor pode liberar sua referência na interface [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) sem chamar o método **Commit**. Não há nenhum recurso para acessar uma linha inserida pelo consumidor no conjunto de linhas e alterar seus valores ou para removê-la individualmente do conjunto de linhas.  
  
 As linhas copiadas em massa são formatadas no servidor para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O formato de linha é afetado por todas as opções que possam ter sido definidas para a conexão ou sessão, como ANSI_PADDING. Essa opção é ativada por padrão para qualquer conexão feita por meio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client.  
  
## <a name="see-also"></a>Consulte também  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
