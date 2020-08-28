---
description: Propriedades ADO
title: Propriedades do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
author: rothja
ms.author: jroth
ms.openlocfilehash: a8a53f4b901209a1ef59be6ca2eb8b531bc52d7c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976277"
---
# <a name="ado-properties"></a>Propriedades ADO

|Propriedade|Descrição|  
|-|-|  
|[AbsolutePage](./absolutepage-property-ado.md)|Indica em qual página o registro atual reside.|  
|[AbsolutePosition](./absoluteposition-property-ado.md)|Indica a posição ordinal do registro atual de um objeto **Recordset** .|  
|[ActiveCommand](./activecommand-property-ado.md)|Indica o objeto de **comando** que criou o objeto **Recordset** associado.|  
|[ActiveConnection](./activeconnection-property-ado.md)|Indica a qual objeto de **conexão** o **comando**, **conjunto de registros**ou objeto de **registro** especificado atualmente pertence.|  
|[ActualSize](./actualsize-property-ado.md)|Indica o comprimento real do valor de um campo.|  
|[Atributos](./attributes-property-ado.md)|Indica uma ou mais características de um objeto.|  
|[BOF e EOF](./bof-eof-properties-ado.md)|A **BOF** indica que a posição atual do registro é anterior ao primeiro registro em um objeto Recordset.<br /><br /> **EOF** indica que a posição atual do registro é posterior ao último registro em um objeto Recordset.|  
|[Indicador](./bookmark-property-ado.md)|Indica um indicador que identifica exclusivamente o registro atual em um objeto **Recordset** ou define o registro atual em um objeto **Recordset** para o registro identificado por um indicador válido.|  
|[CacheSize](./cachesize-property-ado.md)|Indica o número de registros de um objeto **Recordset** que são armazenados em cache localmente na memória.|  
|[Capítulo](./chapter-property-ado.md)|Obtém ou define um objeto de **capítulo** de OLE DB de/em um objeto **ADORecordsetConstruction** .|  
|[CharSet](./charset-property-ado.md)|Indica o conjunto de caracteres no qual o conteúdo de um **fluxo** de texto deve ser traduzido.|  
|[CommandStream](./commandstream-property-ado.md)|Indica o fluxo usado como a entrada para um objeto de **comando** .|  
|[CommandText](./commandtext-property-ado.md)|Indica o texto de um comando a ser emitido em relação a um provedor.|  
|[CommandTimeOut](./commandtimeout-property-ado.md)|Indica por quanto tempo aguardar ao executar um comando antes de encerrar a tentativa e gerar um erro.|  
|[CommandType](./commandtype-property-ado.md)|Indica o tipo de um objeto de **comando** .|  
|[Propriedade ConnectionString](./connectionstring-property-ado.md)|Indica as informações usadas para estabelecer uma conexão com uma fonte de dados.|  
|[ConnectionTimeout](./connectiontimeout-property-ado.md)|Indica por quanto tempo aguardar ao estabelecer uma conexão antes de encerrar a tentativa e gerar um erro.|  
|[Count](./count-property-ado.md)|Indica o número de objetos em uma coleção.|  
|[CursorLocation](./cursorlocation-property-ado.md)|Indica o local do serviço de cursor.|  
|[CursorType](./cursortype-property-ado.md)|Indica o tipo de cursor usado em um objeto **Recordset** .|  
|[DataMember](./datamember-property.md)|Indica o nome do membro de dados que será recuperado do objeto referenciado pela propriedade **DataSource** .|  
|[Fonte](./datasource-property-ado.md)|Indica um objeto que contém dados a serem representados como um objeto **Recordset** .|  
|[DefaultDatabase](./defaultdatabase-property.md)|Indica o banco de dados padrão para um objeto de **conexão** .|  
|[DefinedSize](./definedsize-property.md)|Indica a capacidade de dados de um objeto de **campo** .|  
|[Descrição](./description-property.md)|Descreve um objeto de **erro** .|  
|[Dialeto](./dialect-property.md)|Indica a sintaxe e as regras gerais que o provedor usará para analisar as propriedades **CommandText** ou **CommandStream** .|  
|[Direção](./direction-property.md)|Indica se o **parâmetro** representa um parâmetro de entrada, um parâmetro de saída ou ambos, ou se o parâmetro é o valor de retorno de um procedimento armazenado.|  
|[EditMode](./editmode-property.md)|Indica o status de edição do registro atual.|  
|[EOS](./eos-property.md)|Indica se a posição atual está no final do fluxo.|  
|[Filter](./filter-property.md)|Indica um filtro para dados em um **conjunto de registros**.|  
|[HelpContext e HelpFile](./helpcontext-helpfile-properties.md)|Indica o arquivo de ajuda e o tópico associado a um objeto de **erro** .<br /><br /> O **HelpContextId** retorna uma ID de contexto, como um valor **longo** , para um tópico em um arquivo de ajuda.<br /><br /> **HelpFile** retorna um valor de **cadeia de caracteres** que é avaliado como um caminho totalmente resolvido de um arquivo de ajuda.|  
|[Index](./index-property.md)|Indica o nome do índice atualmente em vigor para um objeto **Recordset** .|  
|[IsolationLevel](./isolationlevel-property.md)|Indica o nível de isolamento para um objeto de **conexão** .|  
|[Item](./item-property-ado.md)|Indica um membro específico de uma coleção, por nome ou número ordinal.|  
|[LineSeparator](./lineseparator-property-ado.md)|Indica o caractere binário a ser usado como separador de linha em objetos de **fluxo** de texto.|  
|[LockType](./locktype-property-ado.md)|Indica o tipo de bloqueios colocados em registros durante a edição.|  
|[MarshalOptions](./marshaloptions-property-ado.md)|Indica quais registros devem ser empacotados de volta para o servidor.|  
|[MaxRecords](./maxrecords-property-ado.md)|Indica o número máximo de registros a serem retornados a um **conjunto de registros** de uma consulta.|  
|[Modo](./mode-property-ado.md)|Indica as permissões disponíveis para modificar dados em um objeto de **conexão**, **registro**ou **fluxo** .|  
|[Nome](./name-property-ado.md)|Indica o nome de um objeto.|  
|[NativeError](./nativeerror-property-ado.md)|Indica o código de erro específico do provedor para um objeto de **erro** específico.|  
|[Número](./number-property-ado.md)|Indica o número que identifica exclusivamente um objeto de **erro** .|  
|[NumericScale](./numericscale-property-ado.md)|Indica a escala de valores numéricos em um objeto de **campo** ou **parâmetro** .|  
|[OriginalValue](./originalvalue-property-ado.md)|Indica o valor de um **campo** que existia no registro antes de qualquer alteração ser feita.|  
|[PageCount](./pagecount-property-ado.md)|Indica quantas páginas de dados o objeto **Recordset** contém.|  
|[PageSize](./pagesize-property-ado.md)|Indica quantos registros representam uma página no conjunto de **registros**.|  
|[ParentRow](./parentrow-property-ado.md)|Define o contêiner de um objeto de **linha** de OLE DB em um objeto **ADORecordConstruction** , para que o pai da linha seja transformado em um objeto de **registro** ADO.|  
|[ParentURL](./parenturl-property-ado.md)|Indica uma cadeia de caracteres de URL absoluta que aponta para o **registro** pai do objeto de **registro** atual.|  
|[Posição](./position-property-ado.md)|Indica a posição atual em um objeto de **fluxo** .|  
|[Precisão](./precision-property-ado.md)|Indica o grau de precisão para valores numéricos em um objeto de **parâmetro** ou para objetos de **campo** numérico.|  
|[Prepared](./prepared-property-ado.md)|Indica se deve salvar uma versão compilada de um comando antes da execução.|  
|[Provedor](./provider-property-ado.md)|Indica o nome do provedor para um objeto de **conexão** .|  
|[RecordCount](./recordcount-property-ado.md)|Indica o número de registros em um objeto **Recordset** .|  
|[RecordType](./recordtype-property-ado.md)|Indica o tipo de objeto de **registro** .|  
|[Fila](./row-property-ado.md)|Obtém ou define um objeto de **linha** de OLE DB de/em um objeto **ADORecordConstruction** .|  
|[RowPosition](./rowposition-property-ado.md)|Obtém ou define um OLE DB objeto de **função** de/em um objeto **ADORecordsetConstruction** .|  
|[Conjunto de linhas](./rowset-property-ado.md)|Obtém ou define um OLE DB objeto de **conjunto de linhas** de/em um objeto **ADORecordsetConstruction** .|  
|[Origem (erro ADO)](./source-property-ado-error.md)|Indica o nome do objeto ou aplicativo que originalmente gerou um erro.|  
|[Origem (registro ADO)](./source-property-ado-record.md)|Indica a entidade representada pelo objeto de **registro** .|  
|[Fonte (conjunto de registros ADO)](./source-property-ado-recordset.md)|Indica a origem dos dados em um objeto **Recordset**|  
|[SQLState](./sqlstate-property.md)|Indica o estado SQL de um objeto de **erro** específico.|  
|[State](./state-property-ado.md)|Indica para todos os objetos aplicáveis se o estado do objeto está aberto ou fechado. Indica para todos os objetos aplicáveis que executam um método assíncrono, se o estado atual do objeto está se conectando, executando ou recuperando|  
|[Status (campo ADO)](./status-property-ado-field.md)|Indica o status de um objeto de **campo** .|  
|[Status (conjunto de registros ADO)](./status-property-ado-recordset.md)|Indica o status do registro atual em relação a atualizações em lotes ou outras operações em massa.|  
|[StayInSync](./stayinsync-property.md)|Indica, em um objeto **Recordset** hierárquico, se a referência aos registros filho subjacentes (ou seja, o *capítulo*) é alterada quando a posição da linha pai é alterada.|  
|[Propriedade Stream](./stream-property.md)|Obtém ou define um objeto de **fluxo** de OLE DB de/em um objeto **ADOStreamConstruction** .|  
|[Tipo](./type-property-ado.md)|Indica o tipo operacional ou o tipo de dados de um **parâmetro**, **campo**ou objeto de **Propriedade** .|  
|[Tipo (fluxo ADO)](./type-property-ado-stream.md)|Indica o tipo de dados contido no **fluxo** (binário ou texto).|  
|[UnderlyingValue](./underlyingvalue-property.md)|Indica o valor atual no banco de dados para um objeto de **campo** .|  
|[Valor](./value-property-ado.md)|Indica o valor atribuído a um **campo**, **parâmetro**ou objeto de **Propriedade** .|  
|[Versão](./version-property-ado.md)|Indica o número de versão do ADO.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](./ado-api-reference.md)   
 [Coleções ADO](./ado-collections.md)   
 [Propriedades dinâmicas do ADO](./ado-dynamic-properties.md)   
 [Constantes enumeradas do ADO](./ado-enumerated-constants.md)   
 [Apêndice B: erros do ADO](../../guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](./ado-events.md)   
 [Métodos do ADO](./ado-methods.md)   
 [Modelo de objeto ADO](./ado-object-model.md)   
 [Objetos e interfaces do ADO](./ado-objects-and-interfaces.md)