---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 67b428a06679bdb0cade14314195d576a1ccc596
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696861"
---
# <a name="ado-methods"></a>Métodos ADO

|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Cria um novo registro para um atualizável **Recordset** objeto.|  
|[Acrescentar](../../../ado/reference/ado-api/append-method-ado.md)|Acrescenta um objeto a uma coleção. Se a coleção estiver **campos**, uma nova **campo** objeto pode ser criado antes que ele é acrescentado à coleção.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Acrescenta dados a um grande de texto ou dados binários **campo**, ou como um **parâmetro** objeto.|  
|[BeginTrans, CommitTrans e RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Gerencia o processamento dentro de transações uma **Conexão** da seguinte maneira:<br /><br /> **BeginTrans** -inicia uma nova transação.<br /><br /> **CommitTrans** – salva as alterações e termina a transação atual. Ele também pode iniciar uma nova transação.<br /><br /> **RollbackTrans** - cancela todas as alterações e termina a transação atual. Ele também pode iniciar uma nova transação.|  
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Cancela a execução de uma chamada de método assíncrono pendente.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Cancela uma atualização em lotes pendentes.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Cancela todas as alterações foram feitas para a linha atual ou nova de um **conjunto de registros** objeto, ou o **campos** coleção de um **registro** objeto antes de chamar o  **Atualização** método.|  
|[Liberada](../../../ado/reference/ado-api/clear-method-ado.md)|Remove todos os **erro** objetos da **erros** coleção.|  
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Cria uma duplicata **conjunto de registros** objeto de uma já existente **Recordset** objeto. Opcionalmente, especifica que o clone ser somente leitura.|  
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Fecha um objeto aberto e todos os objetos dependentes.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Compara dois indicadores e retorna uma indicação dos valores relativos.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Copia um arquivo ou diretório e seu conteúdo, para outro local.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Copia o número especificado de caracteres ou bytes (dependendo da **tipo**) na **Stream** para outra **Stream** objeto.|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Cria um novo **parâmetro** objeto que tem as propriedades especificadas.|  
|[Delete (coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Exclui um objeto a partir de **parâmetros** coleção.|  
|[Excluir (coleção de campos ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Exclui um objeto a partir de **campos** coleção.|  
|[Delete (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Exclui o registro atual ou um grupo de registros.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Exclui um arquivo ou diretório e todos os seus subdiretórios.|  
|[Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Executa a consulta, a instrução SQL ou o procedimento armazenado especificado na **CommandText** propriedade.|  
|[Execute (Conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Executa a consulta especificada, instrução SQL, procedimento armazenado ou texto específico do provedor.|  
|[localizar](../../../ado/reference/ado-api/find-method-ado.md)|Pesquisas de um **Recordset** para a linha que satisfaz os critérios especificados.|  
|[liberar](../../../ado/reference/ado-api/flush-method-ado.md)|Força o conteúdo do **Stream** restantes no buffer ADO para o objeto subjacente com a qual o **Stream** está associado.|  
|[Método get_OLEDBCommand](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Retorna o comando OLE DB subjacentes, propagando primeiro quaisquer informações de parâmetro definido no comando ADO para o comando OLE DB.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Retorna um **conjunto de registros** cujas linhas representam os arquivos e subdiretórios no diretório representado por esse **registro**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Retorna todos os, ou uma parte, o conteúdo de um texto grande ou dados binários **campo** objeto.|  
|[Método GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera o objeto de fonte de dados OLEDB subjacente do provedor de forma.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Recupera vários registros de uma **Recordset** objeto em uma matriz.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Retorna o **Recordset** como uma cadeia de caracteres.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Carrega o conteúdo de um arquivo existente em uma **Stream**.|  
|[Migrar](../../../ado/reference/ado-api/move-method-ado.md)|Move a posição do registro atual em um **Recordset** objeto.|  
|[MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Move para a primeira, última, registro anterior ou seguinte em um especificado **Recordset** objeto e torna esse registro o registro atual.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Move um arquivo, ou um diretório e seu conteúdo para outro local.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Limpa o atual **conjunto de registros** do objeto e retorna o próximo **Recordset** por Avançar até uma série de comandos.|  
|[Abrir (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Abre uma conexão a uma fonte de dados.|  
|[Abrir (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|Abre um existente **registro** de objeto ou cria um novo arquivo ou diretório.|  
|[Abrir (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Abre um cursor.|  
|[Abrir (Stream do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Abre um **Stream** objeto para manipular fluxos de dados de texto ou binárias.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Obtém informações de esquema de banco de dados do provedor.|  
|[Método put_OLEDBCommand](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Esse método não realiza nenhuma operação – ele sempre retorna S_OK.|  
|[Leitura](../../../ado/reference/ado-api/read-method.md)|Lê um número especificado de bytes de um **Stream** objeto.|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Lê um número especificado de caracteres de um texto **Stream** objeto.|  
|[Atualizar](../../../ado/reference/ado-api/refresh-method-ado.md)|Atualiza os objetos em uma coleção para refletir objetos disponíveis do e específicos ao provedor.|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Atualiza os dados em um **Recordset** objeto executar novamente a consulta na qual o objeto se baseia.|  
|[Resync](../../../ado/reference/ado-api/resync-method.md)|Atualiza os dados no atual **conjunto de registros** objeto, ou **campos** coleção de um **registro** objeto do banco de dados subjacente.|  
|[Salvar](../../../ado/reference/ado-api/save-method.md)|Salva o **conjunto de registros** em um arquivo ou **Stream** objeto.|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Salva o conteúdo binário de um **Stream** para um arquivo.|  
|[Busca](../../../ado/reference/ado-api/seek-method.md)|Pesquisa o índice de um **Recordset** para localizar rapidamente a linha que corresponde aos valores especificados e altera a posição da linha atual para aquela linha.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|Define a posição em que é o final do fluxo.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Ignora uma linha inteira durante a leitura de um fluxo de texto.|  
|[Stat](../../../ado/reference/ado-api/stat-method.md)|Obtém informações estatísticas sobre um fluxo aberto.|  
|[Suporta](../../../ado/reference/ado-api/supports-method.md)|Determina se um especificado **Recordset** objeto dá suporte a um determinado tipo de funcionalidade.|  
|[Update (atualizar)](../../../ado/reference/ado-api/update-method.md)|Salva as alterações feitas na linha atual de um **conjunto de registros** objeto, ou o **campos** coleção de um **registro** objeto.|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Grava todas as atualizações em lotes pendentes no disco.|  
|[gravação](../../../ado/reference/ado-api/write-method.md)|Grava dados binários em uma **Stream** objeto.|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|Grava uma cadeia de caracteres de texto especificado para um **Stream** objeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: Erros ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces e os objetos do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
