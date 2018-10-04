---
title: Constantes enumeradas do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a13adf7aa1a769f6e63f9686938cb801cd6383fe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761554"
---
# <a name="ado-enumerated-constants"></a>Constantes enumeradas do ADO
Para ajudar na depuração, as enumerações de ADO listam um valor para cada constante. No entanto, esse valor é puramente comunicado e pode mudar de uma versão do ADO para outro. Seu código deve depender somente o nome, não o valor real de cada constante enumerada.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Para um RDS **conjunto de registros** de objeto, que especifica a prioridade de execução do thread assíncrona que recupera dados.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Especifica quando o **MSDataShape** provedor calcula novamente colunas agregadas e calculadas na hierárquico **conjunto de registros**.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um **Recordset** objeto.|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Especifica se o **UpdateBatch** método é seguido por implícito **ressincronizar** operação de método em caso afirmativo, o escopo da operação.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Especifica quais registros são afetados por uma operação.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Especifica um indicador que indica onde a operação deve ser iniciada.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Especifica como um argumento de comando deve ser interpretado.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Especifica a posição relativa de dois registros representado por seus indicadores.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Especifica as permissões disponíveis para modificar dados em um **Conexão**, abrindo uma **registro**, ou especificando valores para o **modo** propriedade do  **Registro** e **Stream** objetos.|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Especifica se o **aberto** método de um **Conexão** objeto deve retornar após (sincronicamente) ou antes (de forma assíncrona) a conexão seja estabelecida.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Especifica se uma caixa de diálogo deve ser exibida para solicitar parâmetros ausentes ao abrir uma conexão a uma fonte de dados ODBC.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Especifica o comportamento do **CopyRecord** método.|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Especifica o local do mecanismo de cursor.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Especifica qual funcionalidade do **dá suporte a** método deve testar.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Especifica o tipo de cursor usado em uma **Recordset** objeto.|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Especifica o tipo de dados de um **campo**, **parâmetro**, ou **propriedade**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Especifica o status de edição de um registro.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Especifica o tipo de erro de tempo de execução do ADO.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Especifica o motivo que causou um evento ocorra.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Especifica o status atual da execução de um evento.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Especifica como um provedor deve executar um comando.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Especifica os campos especiais, referenciados na **campos** coleção de uma **registro** objeto.|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Especifica um ou mais atributos de uma **campo** objeto.|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Especifica o status de uma **campo** objeto.|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Especifica o grupo de registros a serem filtrados de um **conjunto de registros**.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Especifica quantos registros para recuperar de uma **conjunto de registros**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Especifica o nível de isolamento da transação para um **Conexão** objeto.|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Especifica o caractere usado como um separador de linha no texto **Stream** objetos.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Especifica o tipo de bloqueio colocado em registros durante a edição.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Especifica quais registros devem ser retornados para o servidor.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Especifica o comportamento do **registro** objeto **MoveRecord** método.|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Especifica se um objeto é aberto ou fechado, conectando a uma fonte de dados, executar um comando ou buscar dados.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Especifica os atributos de uma **parâmetro** objeto.|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Especifica se o **parâmetro** representa um parâmetro de entrada, um parâmetro de saída ou ambos, ou se o parâmetro é o valor de retorno de um procedimento armazenado.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Especifica o formato no qual salvar uma **conjunto de registros**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Especifica a posição atual do ponteiro do registro dentro de uma **conjunto de registros**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Especifica os atributos de uma **propriedade** objeto.|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Especifica para o **registro** objeto **abra** método se existente **registro** deve ser aberta, ou um novo **registro** deve ser criado.|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Especifica opções para abrir um **registro**. Esses valores podem ser combinados usando um operador OR.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Especifica o status de um registro em relação a atualizações em lotes e outras operações em massa.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Especifica o tipo de **registro** objeto.|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Especifica se os valores subjacentes são substituídos por uma chamada para **ressincronizar**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Especifica se um arquivo deve ser criado ou substituído quando salvar uma **Stream** objeto. Os valores podem ser combinados com um operador AND.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Especifica o tipo de esquema **conjunto de registros** que o **OpenSchema** recupera do método. Especifica a direção de uma pesquisa de registro dentro de uma **conjunto de registros**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Especifica a direção de uma pesquisa de registro dentro de uma **conjunto de registros**. Especifica o tipo de **busca** para executar.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Especifica o tipo de **busca** para executar. Especifica opções para abrir um **Stream** objeto. Os valores podem ser combinados com um operador AND.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Especifica opções para abrir um **Stream** objeto. Os valores podem ser combinados com um operador AND. Especifica se o fluxo inteiro ou a próxima linha deve ser lidos de um **Stream** objeto.|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Especifica se o fluxo inteiro ou a próxima linha deve ser lidos de um **Stream** objeto. Especifica o tipo de dados armazenados em um **Stream** objeto.|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Especifica o tipo de dados armazenados em um **Stream** objeto. Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um **Stream** objeto.|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um **Stream** objeto. Especifica o formato ao recuperar um **Recordset** como uma cadeia de caracteres.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Especifica o formato ao recuperar um **Recordset** como uma cadeia de caracteres. Especifica os atributos de transação de um **Conexão** objeto.|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Especifica os atributos de transação de um **Conexão** objeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Apêndice b: erros de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces e os objetos do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
