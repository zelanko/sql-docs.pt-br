---
title: Interface IMDEmbedded | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3973640b4a4efca789ec107c1c1f086801cac234
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115518"
---
# <a name="imdembedded-interface"></a>Interface IMDEmbedded
  A interface IMDEmbedded é uma interface pública usada para gerenciar um banco de dados do PowerPivot inserido ou um banco de dados modelo de tabela. A interface herda da interface `IPersistStream`. A interface permite as seguintes operações:  
  
-   Obter um identificador do fluxo inserido no documento contêiner.  
  
-   Definir a URL do documento contêiner.  
  
-   Definir um sinalizador para indicar se o aplicativo inserido está em um ambiente hospedado.  
  
-   Definir o caminho para os arquivos temporários usados pelo aplicativo inserido.  
  
-   Cancelar a operação inserida atual.  
  
-   Obter o tamanho estimado (em bytes) do fluxo para salvar o objeto inserido. Herdado de `IPersistStream`.  
  
-   Verificar se o banco de dados inserido foi alterado após ser salvo pela última vez. Herdado de `IPersistStream`.  
  
-   Carregar o banco de dados inserido para o mecanismo local ou em processo. Herdado de `IPersistStream`.  
  
-   Salvar o banco de dados local ou em processo para o fluxo inserido no documento contêiner. Herdado de `IPersistStream`.  
  
## <a name="reference"></a>Referência  
 A referência a seguir documentos a `IMDEmbedded` interface como apresentado em **msmd. h** arquivo de cabeçalho.  
  
### <a name="source-file-pxoembeddeddataidl"></a>Arquivo de origem: PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>Description  
 Obtém o identificador usado pelo aplicativo de host para o fluxo inserido no documento contêiner.  
  
#### <a name="parameters"></a>Parâmetros  
 *out_pbstrStreamId*  
 Especifica o local do identificador de fluxo.  
  
#### <a name="return-value"></a>Valor retornado  
 `S_OK`  
 O identificador de fluxo foi retornado com êxito.  
  
 `S_FALSE`  
 Não há nenhum identificador de fluxo.  
  
 `E_FAIL`  
 Erro ao acessar o identificador de fluxo.  
  
#### <a name="remarks"></a>Remarks  
 Para verificar se a conexão atual contém um banco de dados inserido, o usuário deve verificar o valor da propriedade DBPROP_MSMD_EMBEDDED_DATA nas propriedades de conexão OLE DB.  
  
 Os valores possíveis para DBPROP_MSMD_EMBEDDED_DATA são:  
  
|Nome|Valor|Definição|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|Nenhum banco de dados inserido disponível|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|O aplicativo atual contém o banco de dados inserido|  
|DBPROPVAL_EMBED_LINKED|0x02|O banco de dados inserido está hospedado em um aplicativo remoto (p. ex., SharePoint Server)|  
  
#### <a name="source"></a>Origem  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>Description  
 Define a URL para o arquivo que contém o fluxo inserido.  
  
#### <a name="parameters"></a>Parâmetros  
 *in_bstrURL*  
 Especifica a URL para o documento contêiner.  
  
#### <a name="return-value"></a>Valor retornado  
 `S_OK`  
 A URL do contêiner foi definida com êxito.  
  
 `E_FAIL`  
 Erro ao definir a URL do contêiner.  
  
#### <a name="source"></a>Origem  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>Description  
 Definir um sinalizador para indicar se o aplicativo inserido está em um ambiente hospedado.  
  
#### <a name="parameters"></a>Parâmetros  
 *in_ftHosted*  
 TRUE se o chamador estiver hospedado em um aplicativo de serviço (como o IIS).  
  
#### <a name="return-value"></a>Valor retornado  
 `S_OK`  
 O sinalizador foi definido com êxito.  
  
 `E_FAIL`  
 Erro ao definir o sinalizador.  
  
#### <a name="source"></a>Origem  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>Description  
 Definir o caminho para os arquivos temporários usados pelo aplicativo inserido.  
  
#### <a name="parameters"></a>Parâmetros  
 *in_bstrPath*  
 O caminho usado pelo aplicativo de host para arquivos temporários.  
  
#### <a name="return-value"></a>Valor retornado  
 `S_OK`  
 O diretório de arquivos temporários foi definido com êxito.  
  
 `E_FAIL`  
 Erro ao definir o caminho.  
  
#### <a name="source"></a>Origem  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Description  
 Cancela a operação de banco de dados inserida atual.  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum.  
  
#### <a name="return-value"></a>Valor retornado  
 `S_OK`  
 A operação foi cancelada com êxito.  
  
 `DB_E_CANTCANCEL`  
 Nenhuma operação cancelável está em andamento atualmente.  
  
 `E_FAIL`  
 Erro ao cancelar a operação inserida.  
  
#### <a name="source"></a>Origem  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>Description  
 Obtém o tamanho estimado (em bytes) do fluxo para salvar o objeto inserido. Herdado de `IPersistStream`.  
  
#### <a name="parameters"></a>Parâmetros  
 *in_bstrPath*  
 O tamanho estimado (em bytes) da imagem de banco de dados inserida.  
  
#### <a name="return-value"></a>Valor retornado  
 `S_OK`  
 O tamanho foi obtido com êxito.  
  
 `E_FAIL`  
 Erro ao obter o tamanho.  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Description  
 Verifica se o banco de dados inserido foi alterado após ser salvo pela última vez. Herdado de `IPersistStream`.  
  
#### <a name="parameters"></a>Parâmetros  
 none  
  
#### <a name="return-values"></a>Valor(es) de retorno  
 `S_OK`  
 O banco de dados foi alterado desde que foi salvo pela última vez.  
  
 `S_FALSE`  
 O banco de dados não foi alterado desde que foi salvo pela última vez.  
  
 `E_FAIL`  
 Erro ao obter o estado do banco de dados.  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Description  
 Carrega o banco de dados inserido para o mecanismo local ou em processo. Herdado de `IPersistStream`.  
  
#### <a name="parameters"></a>Parâmetros  
 *in_pStm*  
 Um ponteiro para uma interface de fluxo da qual deverá ser carregado o banco de dados inserido.  
  
#### <a name="return-values"></a>Valor(es) de retorno  
 `S_OK`  
 O banco de dados foi carregado com êxito.  
  
 `E_OUTOFMEMORY`  
 Memória insuficiente para carregar o banco de dados.  
  
 `E_FAIL`  
 Erro diferente de `E_OUTOFMEMORY` ao carregar o banco de dados.  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Description  
 Salva o banco de dados local ou em processo para o fluxo inserido no documento contêiner. Herdado de `IPersistStream`.  
  
#### <a name="parameters"></a>Parâmetros  
 *in_pStm*  
 Um ponteiro para uma interface de fluxo na qual deverá ser salvo o banco de dados inserido.  
  
 *in_fClearDirty*  
 Um sinalizador que indica se o sinalizador sujo deve ser limpo após esta operação.  
  
#### <a name="return-values"></a>Valor(es) de retorno  
 `S_OK`  
 O banco de dados foi salvo com êxito.  
  
 `STG_E_CANTSAVE`  
 Erro diferente de `STG_E_MEDIUMFULL` ao salvar o banco de dados.  
  
 `STG_E_MEDIUMFULL`  
 Não foi possível salvar o banco de dados porque não há espaço remanescente no dispositivo de armazenamento.  
  
  