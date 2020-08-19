---
description: Métodos ADO
title: Métodos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: rothja
ms.author: jroth
ms.openlocfilehash: 10f9aaf7aefa87586df77dd0da5ac1be336d4f53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451378"
---
# <a name="ado-methods"></a>Métodos ADO

|Método|Descrição|  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Cria um novo registro para um objeto **Recordset** atualizável.|  
|[Append](../../../ado/reference/ado-api/append-method-ado.md)|Anexa um objeto a uma coleção. Se a coleção for de **campos**, um novo objeto de **campo** poderá ser criado antes de ser anexado à coleção.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Anexa dados a um **campo**de dados binário ou de texto grande ou a um objeto de **parâmetro** .|  
|[BeginTrans, CommitTrans e RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Gerencia o processamento de transações dentro de um objeto de **conexão** da seguinte maneira:<br /><br /> **BeginTrans** – inicia uma nova transação.<br /><br /> **CommitTrans** -salva todas as alterações e encerra a transação atual. Ele também pode iniciar uma nova transação.<br /><br /> **RollbackTrans** -cancela as alterações e encerra a transação atual. Ele também pode iniciar uma nova transação.|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Cancela a execução de uma chamada de método pendente e assíncrona.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Cancela uma atualização de lote pendente.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Cancela as alterações feitas na linha atual ou nova de um objeto **Recordset** ou na coleção **Fields** de um objeto **Record** , antes de chamar o método **Update** .|  
|[Limpar](../../../ado/reference/ado-api/clear-method-ado.md)|Remove todos os objetos de **erro** da coleção de **erros** .|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Cria um objeto **Recordset** duplicado a partir de um objeto **Recordset** existente. Opcionalmente, especifica que o clone é somente leitura.|  
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Fecha um objeto aberto e quaisquer objetos dependentes.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Compara dois indicadores e retorna uma indicação de seus valores relativos.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Copia um arquivo ou diretório e seu conteúdo para outro local.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Copia o número especificado de caracteres ou bytes (dependendo do **tipo**) no **fluxo** para outro objeto de **fluxo** .|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Cria um novo objeto de **parâmetro** que tem as propriedades especificadas.|  
|[Delete (coleção de parâmetros do ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Exclui um objeto da coleção de **parâmetros** .|  
|[Delete (coleção de campos do ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Exclui um objeto da coleção **Fields** .|  
|[Excluir (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Exclui o registro atual ou um grupo de registros.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Exclui um arquivo ou diretório e todos os seus subdiretórios.|  
|[Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Executa a consulta, a instrução SQL ou o procedimento armazenado especificado na propriedade **CommandText** .|  
|[Executar (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Executa a consulta especificada, a instrução SQL, o procedimento armazenado ou o texto específico do provedor.|  
|[Localizar](../../../ado/reference/ado-api/find-method-ado.md)|Pesquisa um **conjunto de registros** para a linha que satisfaz os critérios especificados.|  
|[Liberar](../../../ado/reference/ado-api/flush-method-ado.md)|Força o conteúdo do **fluxo** restante no buffer do ADO para o objeto subjacente ao qual o **fluxo** está associado.|  
|[Método get_OLEDBCommand](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Retorna o comando OLEDB subjacente, primeiro propagando todas as informações de parâmetro definidas no comando ADO para o comando OLEDB.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Retorna um **conjunto de registros** cujas linhas representam os arquivos e subdiretórios no diretório representado por esse **registro**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Retorna todos, ou uma parte, do conteúdo de um objeto de **campo** de dados binário ou de texto grande.|  
|[Método GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera o objeto de fonte de dados OLEDB subjacente do provedor de forma.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Recupera vários registros de um objeto **Recordset** em uma matriz.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Retorna o **conjunto de registros** como uma cadeia de caracteres.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Carrega o conteúdo de um arquivo existente em um **fluxo**.|  
|[Mover](../../../ado/reference/ado-api/move-method-ado.md)|Move a posição do registro atual em um objeto **Recordset** .|  
|[MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Move para o primeiro, último, próximo ou registro anterior em um objeto **Recordset** especificado e torna esse registro o registro atual.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Move um arquivo ou um diretório e seu conteúdo para outro local.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Limpa o objeto **Recordset** atual e retorna o próximo **conjunto de registros** avançando por meio de uma série de comandos.|  
|[Abrir (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Abre uma conexão com uma fonte de dados.|  
|[Abrir (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|Abre um objeto de **registro** existente ou cria um novo arquivo ou diretório.|  
|[Abrir (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Abre um cursor.|  
|[Abrir (fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Abre um objeto de **fluxo** para manipular fluxos de dados binários ou de texto.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Obtém informações de esquema de banco de dados do provedor.|  
|[Método put_OLEDBCommand](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Esse método não executa nenhuma operação – ele sempre retorna S_OK.|  
|[Ler](../../../ado/reference/ado-api/read-method.md)|Lê um número especificado de bytes de um objeto de **fluxo** .|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Lê um número especificado de caracteres de um objeto de **fluxo** de texto.|  
|[Atualizar](../../../ado/reference/ado-api/refresh-method-ado.md)|Atualiza os objetos em uma coleção para refletir objetos disponíveis de e específicos para o provedor.|  
|[Repita](../../../ado/reference/ado-api/requery-method.md)|Atualiza os dados em um objeto de **conjunto de registros** executando novamente a consulta na qual o objeto se baseia.|  
|[Sincronizar novamente](../../../ado/reference/ado-api/resync-method.md)|Atualiza os dados no objeto **Recordset** atual ou na coleção **Fields** de um objeto **Record** , do banco de dados subjacente.|  
|[Salvar](../../../ado/reference/ado-api/save-method.md)|Salva o **conjunto de registros** em um objeto de arquivo ou **fluxo** .|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Salva o conteúdo binário de um **fluxo** em um arquivo.|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|Pesquisa o índice de um **conjunto de registros** para localizar rapidamente a linha que corresponde aos valores especificados e altera a posição da linha atual para essa linha.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|Define a posição que é o final do fluxo.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Ignora uma linha inteira ao ler um fluxo de texto.|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|Obtém informações estatísticas sobre um fluxo aberto.|  
|[Suporta](../../../ado/reference/ado-api/supports-method.md)|Determina se um objeto **Recordset** especificado dá suporte a um tipo específico de funcionalidade.|  
|[Atualização](../../../ado/reference/ado-api/update-method.md)|Salva as alterações feitas na linha atual de um objeto **Recordset** ou a coleção **Fields** de um objeto **Record** .|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Grava todas as atualizações de lote pendentes no disco.|  
|[Gravar](../../../ado/reference/ado-api/write-method.md)|Grava dados binários em um objeto de **fluxo** .|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|Grava uma cadeia de caracteres de texto especificada em um objeto de **fluxo** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
