---
description: Métodos ADO
title: Métodos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 13e126f070f188e47582227fabf4a1e37d6901a3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976367"
---
# <a name="ado-methods"></a>Métodos ADO

|Método|Descrição|  
|-|-|  
|[AddNew](./addnew-method-ado.md)|Cria um novo registro para um objeto **Recordset** atualizável.|  
|[Append](./append-method-ado.md)|Anexa um objeto a uma coleção. Se a coleção for de **campos**, um novo objeto de **campo** poderá ser criado antes de ser anexado à coleção.|  
|[AppendChunk](./appendchunk-method-ado.md)|Anexa dados a um **campo**de dados binário ou de texto grande ou a um objeto de **parâmetro** .|  
|[BeginTrans, CommitTrans e RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)|Gerencia o processamento de transações dentro de um objeto de **conexão** da seguinte maneira:<br /><br /> **BeginTrans** – inicia uma nova transação.<br /><br /> **CommitTrans** -salva todas as alterações e encerra a transação atual. Ele também pode iniciar uma nova transação.<br /><br /> **RollbackTrans** -cancela as alterações e encerra a transação atual. Ele também pode iniciar uma nova transação.|  
|[Cancelar](./cancel-method-ado.md)|Cancela a execução de uma chamada de método pendente e assíncrona.|  
|[CancelBatch](./cancelbatch-method-ado.md)|Cancela uma atualização de lote pendente.|  
|[CancelUpdate](./cancelupdate-method-ado.md)|Cancela as alterações feitas na linha atual ou nova de um objeto **Recordset** ou na coleção **Fields** de um objeto **Record** , antes de chamar o método **Update** .|  
|[Limpar](./clear-method-ado.md)|Remove todos os objetos de **erro** da coleção de **erros** .|  
|[Clone](./clone-method-ado.md)|Cria um objeto **Recordset** duplicado a partir de um objeto **Recordset** existente. Opcionalmente, especifica que o clone é somente leitura.|  
|[Fechar](./close-method-ado.md)|Fecha um objeto aberto e quaisquer objetos dependentes.|  
|[CompareBookmarks](./comparebookmarks-method-ado.md)|Compara dois indicadores e retorna uma indicação de seus valores relativos.|  
|[CopyRecord](./copyrecord-method-ado.md)|Copia um arquivo ou diretório e seu conteúdo para outro local.|  
|[CopyTo](./copyto-method-ado.md)|Copia o número especificado de caracteres ou bytes (dependendo do **tipo**) no **fluxo** para outro objeto de **fluxo** .|  
|[CreateParameter](./createparameter-method-ado.md)|Cria um novo objeto de **parâmetro** que tem as propriedades especificadas.|  
|[Delete (coleção de parâmetros do ADO)](./delete-method-ado-parameters-collection.md)|Exclui um objeto da coleção de **parâmetros** .|  
|[Delete (coleção de campos do ADO)](./delete-method-ado-fields-collection.md)|Exclui um objeto da coleção **Fields** .|  
|[Excluir (conjunto de registros ADO)](./delete-method-ado-recordset.md)|Exclui o registro atual ou um grupo de registros.|  
|[DeleteRecord](./deleterecord-method-ado.md)|Exclui um arquivo ou diretório e todos os seus subdiretórios.|  
|[Execute (comando ADO)](./execute-method-ado-command.md)|Executa a consulta, a instrução SQL ou o procedimento armazenado especificado na propriedade **CommandText** .|  
|[Executar (conexão ADO)](./execute-method-ado-connection.md)|Executa a consulta especificada, a instrução SQL, o procedimento armazenado ou o texto específico do provedor.|  
|[Localizar](./find-method-ado.md)|Pesquisa um **conjunto de registros** para a linha que satisfaz os critérios especificados.|  
|[Liberar](./flush-method-ado.md)|Força o conteúdo do **fluxo** restante no buffer do ADO para o objeto subjacente ao qual o **fluxo** está associado.|  
|[Método get_OLEDBCommand](./get-oledbcommand-method.md)|Retorna o comando OLEDB subjacente, primeiro propagando todas as informações de parâmetro definidas no comando ADO para o comando OLEDB.|  
|[GetChildren](./getchildren-method-ado.md)|Retorna um **conjunto de registros** cujas linhas representam os arquivos e subdiretórios no diretório representado por esse **registro**.|  
|[GetChunk](./getchunk-method-ado.md)|Retorna todos, ou uma parte, do conteúdo de um objeto de **campo** de dados binário ou de texto grande.|  
|[Método GetDataProviderDSO](./getdataproviderdso-method.md)|Recupera o objeto de fonte de dados OLEDB subjacente do provedor de forma.|  
|[GetRows](./getrows-method-ado.md)|Recupera vários registros de um objeto **Recordset** em uma matriz.|  
|[GetString](./getstring-method-ado.md)|Retorna o **conjunto de registros** como uma cadeia de caracteres.|  
|[LoadFromFile](./loadfromfile-method-ado.md)|Carrega o conteúdo de um arquivo existente em um **fluxo**.|  
|[Mover](./move-method-ado.md)|Move a posição do registro atual em um objeto **Recordset** .|  
|[MoveFirst, MoveLast, MoveNext e MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Move para o primeiro, último, próximo ou registro anterior em um objeto **Recordset** especificado e torna esse registro o registro atual.|  
|[MoveRecord](./moverecord-method-ado.md)|Move um arquivo ou um diretório e seu conteúdo para outro local.|  
|[NextRecordset](./nextrecordset-method-ado.md)|Limpa o objeto **Recordset** atual e retorna o próximo **conjunto de registros** avançando por meio de uma série de comandos.|  
|[Abrir (conexão ADO)](./open-method-ado-connection.md)|Abre uma conexão com uma fonte de dados.|  
|[Abrir (registro ADO)](./open-method-ado-record.md)|Abre um objeto de **registro** existente ou cria um novo arquivo ou diretório.|  
|[Abrir (conjunto de registros ADO)](./open-method-ado-recordset.md)|Abre um cursor.|  
|[Abrir (fluxo do ADO)](./open-method-ado-stream.md)|Abre um objeto de **fluxo** para manipular fluxos de dados binários ou de texto.|  
|[OpenSchema](./openschema-method.md)|Obtém informações de esquema de banco de dados do provedor.|  
|[Método put_OLEDBCommand](./put-oledbcommand-method.md)|Esse método não executa nenhuma operação – ele sempre retorna S_OK.|  
|[Ler](./read-method.md)|Lê um número especificado de bytes de um objeto de **fluxo** .|  
|[ReadText](./readtext-method.md)|Lê um número especificado de caracteres de um objeto de **fluxo** de texto.|  
|[Atualizar](./refresh-method-ado.md)|Atualiza os objetos em uma coleção para refletir objetos disponíveis de e específicos para o provedor.|  
|[Repita](./requery-method.md)|Atualiza os dados em um objeto de **conjunto de registros** executando novamente a consulta na qual o objeto se baseia.|  
|[Sincronizar novamente](./resync-method.md)|Atualiza os dados no objeto **Recordset** atual ou na coleção **Fields** de um objeto **Record** , do banco de dados subjacente.|  
|[Salvar](./save-method.md)|Salva o **conjunto de registros** em um objeto de arquivo ou **fluxo** .|  
|[SaveToFile](./savetofile-method.md)|Salva o conteúdo binário de um **fluxo** em um arquivo.|  
|[Seek](./seek-method.md)|Pesquisa o índice de um **conjunto de registros** para localizar rapidamente a linha que corresponde aos valores especificados e altera a posição da linha atual para essa linha.|  
|[SetEOS](./seteos-method.md)|Define a posição que é o final do fluxo.|  
|[SkipLine](./skipline-method.md)|Ignora uma linha inteira ao ler um fluxo de texto.|  
|[Stat](./stat-method.md)|Obtém informações estatísticas sobre um fluxo aberto.|  
|[Suporta](./supports-method.md)|Determina se um objeto **Recordset** especificado dá suporte a um tipo específico de funcionalidade.|  
|[Atualização](./update-method.md)|Salva as alterações feitas na linha atual de um objeto **Recordset** ou a coleção **Fields** de um objeto **Record** .|  
|[UpdateBatch](./updatebatch-method.md)|Grava todas as atualizações de lote pendentes no disco.|  
|[Gravar](./write-method.md)|Grava dados binários em um objeto de **fluxo** .|  
|[WriteText](./writetext-method.md)|Grava uma cadeia de caracteres de texto especificada em um objeto de **fluxo** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](./ado-api-reference.md)   
 [Coleções ADO](./ado-collections.md)   
 [Propriedades dinâmicas do ADO](./ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](./ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](./ado-events.md)   
 [Modelo de objeto ADO](./ado-object-model.md)   
 [Objetos e interfaces do ADO](./ado-objects-and-interfaces.md)   
 [Propriedades ADO](./ado-properties.md)