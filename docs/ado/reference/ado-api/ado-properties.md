---
title: Propriedades ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f24ffa490ac8ae5b88809b89eed8a188b86fabb
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044671"
---
# <a name="ado-properties"></a>Propriedades ADO

|||  
|-|-|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|Indica em qual página de registro atual reside.|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|Indica a posição ordinal do registro atual de um **Recordset** objeto.|  
|[ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md)|Indica o **comando** objeto que criou associado **Recordset** objeto.|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|Indica para o qual **Conexão** do objeto especificado **comando**, **conjunto de registros**, ou **registro** no momento, o objeto pertence.|  
|[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)|Indica o comprimento real de um valor de campo.|  
|[Atributos](../../../ado/reference/ado-api/attributes-property-ado.md)|Indica uma ou mais características de um objeto.|  
|[BOF e EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|**BOF** indica que a posição do registro atual está antes do primeiro registro em um objeto Recordset.<br /><br /> **EOF** indica que a posição do registro atual é após o último registro em um objeto Recordset.|  
|[Indicador](../../../ado/reference/ado-api/bookmark-property-ado.md)|Indica um marcador que identifica exclusivamente o registro atual em um **conjunto de registros** do objeto ou define o registro atual em um **Recordset** objeto para o registro identificado por um indicador válido.|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|Indica o número de registros de uma **Recordset** objeto armazenados em cache localmente na memória.|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Obtém ou define um banco de dados OLE **capítulo** objeto de/em uma **ADORecordsetConstruction** objeto.|  
|[CharSet](../../../ado/reference/ado-api/charset-property-ado.md)|Indica o caractere definido na qual o conteúdo de um texto **Stream** devem ser traduzidos.|  
|[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)|Indica o fluxo usado como entrada para um **comando** objeto.|  
|[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)|Indica o texto de um comando ser emitido para um provedor.|  
|[CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md)|Indica o tempo de espera durante a execução de um comando antes de encerrar a tentativa e gerar um erro.|  
|[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)|Indica o tipo de um **comando** objeto.|  
|[Propriedade ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)|Indica as informações usadas para estabelecer uma conexão a uma fonte de dados.|  
|[ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)|Indica por quanto tempo a esperar ao estabelecer uma conexão antes de encerrar a tentativa e gerar um erro.|  
|[Count](../../../ado/reference/ado-api/count-property-ado.md)|Indica o número de objetos em uma coleção.|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|Indica o local do serviço de cursor.|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Indica o tipo de cursor usado em uma **Recordset** objeto.|  
|[DataMember](../../../ado/reference/ado-api/datamember-property.md)|Indica o nome do membro de dados que será recuperado do objeto referenciado pelo **fonte de dados** propriedade.|  
|[DataSource](../../../ado/reference/ado-api/datasource-property-ado.md)|Indica um objeto que contém dados a ser representado como uma **Recordset** objeto.|  
|[DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)|Indica o banco de dados padrão para um **Conexão** objeto.|  
|[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)|Indica a capacidade de dados de um **campo** objeto.|  
|[Descrição](../../../ado/reference/ado-api/description-property.md)|Descreve um **erro** objeto.|  
|[Dialeto](../../../ado/reference/ado-api/dialect-property.md)|Indica a sintaxe e regras gerais que o provedor usará para analisar a **CommandText** ou **CommandStream** propriedades.|  
|[Direção](../../../ado/reference/ado-api/direction-property.md)|Indica se o **parâmetro** representa um parâmetro de entrada, um parâmetro de saída ou ambos, ou se o parâmetro é o valor de retorno de um procedimento armazenado.|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|Indica o status de edição do registro atual.|  
|[EOS](../../../ado/reference/ado-api/eos-property.md)|Indica se a posição atual está no final do fluxo.|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|Indica um filtro para os dados em um **conjunto de registros**.|  
|[HelpContext e HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)|Indica o arquivo de Ajuda e o tópico associado a um **erro** objeto.<br /><br /> **IdentificaçãoDoContextoDaAjuda** retorna uma ID de contexto, como uma **longo** valor para um tópico em um arquivo de Ajuda.<br /><br /> **HelpFile** retorna um **cadeia de caracteres** valor que é avaliada para um caminho totalmente resolvido de um arquivo de Ajuda.|  
|[Index](../../../ado/reference/ado-api/index-property.md)|Indica o nome do índice atualmente em vigor para um **Recordset** objeto.|  
|[IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md)|Indica o nível de isolamento para um **Conexão** objeto.|  
|[Item](../../../ado/reference/ado-api/item-property-ado.md)|Indica um membro específico de uma coleção por nome ou número ordinal.|  
|[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)|Indica o caractere binário a ser usado como o separador de linha no texto **Stream** objetos.|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Indica o tipo de bloqueios são colocados nos registros durante a edição.|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|Indica quais registros devem ser empacotados de volta para o servidor.|  
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|Indica o número máximo de registros a serem retornados para um **conjunto de registros** de uma consulta.|  
|[Modo](../../../ado/reference/ado-api/mode-property-ado.md)|Indica as permissões disponíveis para modificar dados em um **Conexão**, **registro**, ou **Stream** objeto.|  
|[Nome](../../../ado/reference/ado-api/name-property-ado.md)|Indica o nome de um objeto.|  
|[NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)|Indica o código de erro específico do provedor para um determinado **erro** objeto.|  
|[número](../../../ado/reference/ado-api/number-property-ado.md)|Indica o número que identifica exclusivamente um **erro** objeto.|  
|[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)|Indica a escala de valores numéricos em uma **parâmetro** ou **campo** objeto.|  
|[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)|Indica o valor de uma **campo** que existiam no registro antes de todas as alterações foram feitas.|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|Indica quantas páginas de dados do **Recordset** objeto contém.|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|Indica o número de registros representa uma página na **conjunto de registros**.|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|Define o contêiner de um banco de dados OLE **linha** do objeto em um **ADORecordConstruction** objeto, de modo que o pai da linha é transformado em ADO **registro** objeto.|  
|[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)|Indica uma cadeia de caracteres de URL absoluta que aponta para o pai **registro** atual **registro** objeto.|  
|[Posição](../../../ado/reference/ado-api/position-property-ado.md)|Indica a posição atual dentro de um **Stream** objeto.|  
|[Precisão](../../../ado/reference/ado-api/precision-property-ado.md)|Indica o grau de precisão para valores numéricos em uma **parâmetro** objeto ou de numérica **campo** objetos.|  
|[Preparado](../../../ado/reference/ado-api/prepared-property-ado.md)|Indica se é necessário salvar uma versão compilada de um comando antes da execução.|  
|[Provedor](../../../ado/reference/ado-api/provider-property-ado.md)|Indica o nome do provedor para uma **Conexão** objeto.|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|Indica o número de registros em uma **Recordset** objeto.|  
|[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)|Indica o tipo de **registro** objeto.|  
|[Row](../../../ado/reference/ado-api/row-property-ado.md)|Obtém ou define um banco de dados OLE **linha** objeto de/em uma **ADORecordConstruction** objeto.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Obtém ou define um banco de dados OLE **RowPosition** objeto de/em uma **ADORecordsetConstruction** objeto.|  
|[Rowset](../../../ado/reference/ado-api/rowset-property-ado.md)|Obtém ou define um banco de dados OLE **conjunto de linhas** objeto de/em uma **ADORecordsetConstruction** objeto.|  
|[Fonte (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)|Indica o nome do objeto ou aplicativo que originalmente gerou um erro.|  
|[Fonte (registro ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)|Indica a entidade representada pela **registro** objeto.|  
|[Fonte (conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)|Indica a origem para os dados em um **Recordset** objeto|  
|[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)|Indica o estado SQL para um determinado **erro** objeto.|  
|[Estado](../../../ado/reference/ado-api/state-property-ado.md)|Indica para todos os objetos aplicáveis se o estado do objeto é aberto ou fechado. Indica para todos os objetos aplicáveis a execução de um método assíncrono, se o estado atual do objeto de conexão, execução ou recuperando|  
|[Status (campo ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)|Indica o status de uma **campo** objeto.|  
|[Status (conjunto de registros ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)|Indica o status do registro atual em relação a atualizações em lotes ou outras operações em massa.|  
|[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)|Indica, em modo hierárquico **conjunto de registros** objeto, se a referência para os registros filho subjacente (ou seja, o *capítulo*) é alterado quando a linha pai posicione as alterações.|  
|[Propriedade Stream](../../../ado/reference/ado-api/stream-property.md)|Obtém ou define um banco de dados OLE **Stream** objeto de/em uma **ADOStreamConstruction** objeto.|  
|[Tipo](../../../ado/reference/ado-api/type-property-ado.md)|Indica o tipo de dados ou tipo operacional de um **parâmetro**, **campo**, ou **propriedade** objeto.|  
|[Tipo (Stream do ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)|Indica o tipo de dados que estão contidos na **Stream** (binários ou texto).|  
|[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)|Indica o valor atual no banco de dados para um **campo** objeto.|  
|[Value](../../../ado/reference/ado-api/value-property-ado.md)|Indica o valor atribuído a um **campo**, **parâmetro**, ou **propriedade** objeto.|  
|[Versão](../../../ado/reference/ado-api/version-property-ado.md)|Indica o número de versão do ADO.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apêndice b: Erros ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)
