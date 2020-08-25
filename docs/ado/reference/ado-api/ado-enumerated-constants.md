---
description: Constantes enumeradas do ADO
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c2b7890cc9926025e7662e8571fb79309590f9de
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776673"
---
# <a name="ado-enumerated-constants"></a>Constantes enumeradas do ADO
Para auxiliar na depuração, as enumerações do ADO listam um valor para cada constante. No entanto, esse valor é puramente consultivo e pode ser alterado de uma versão do ADO para outra. Seu código só deve depender do nome, não do valor real, de cada constante enumerada.  
  
|Constante|DESCRIÇÃO|  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](./adcprop-asyncthreadpriority-enum.md)|Para um objeto de **conjunto de registros** do RDS, especifica a prioridade de execução do thread assíncrono que recupera dados.|  
|[ADCPROP_AUTORECALC_ENUM](./adcprop-autorecalc-enum.md)|Especifica quando o provedor **MSDataShape** recalcula as colunas agregadas e calculadas em um **conjunto de registros**hierárquico.|  
|[ADCPROP_UPDATECRITERIA_ENUM](./adcprop-updatecriteria-enum.md)|Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um objeto **Recordset** .|  
|[ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md)|Especifica se o método **UpdateBatch** é seguido por uma operação de método de **ressincronização** implícita e, nesse caso, o escopo dessa operação.|  
|[AffectEnum](./affectenum.md)|Especifica quais registros são afetados por uma operação.|  
|[BookmarkEnum](./bookmarkenum.md)|Especifica um indicador que indica onde a operação deve começar.|  
|[CommandTypeEnum](./commandtypeenum.md)|Especifica como um argumento de comando deve ser interpretado.|  
|[CompareEnum](./compareenum.md)|Especifica a posição relativa de dois registros representados por seus indicadores.|  
|[ConnectModeEnum](./connectmodeenum.md)|Especifica as permissões disponíveis para modificar dados em uma **conexão**, abrir um **registro**ou especificar valores para a propriedade **Mode** dos objetos **Record** e **Stream** .|  
|[ConnectOptionEnum](./connectoptionenum.md)|Especifica se o método **Open** de um objeto de **conexão** deve retornar após (sincronamente) ou antes (assincronamente) que a conexão seja estabelecida.|  
|[ConnectPromptEnum](./connectpromptenum.md)|Especifica se uma caixa de diálogo deve ser exibida para solicitar parâmetros ausentes ao abrir uma conexão com uma fonte de dados ODBC.|  
|[CopyRecordOptionsEnum](./copyrecordoptionsenum.md)|Especifica o comportamento do método **CopyRecord** .|  
|[CursorLocationEnum](./cursorlocationenum.md)|Especifica o local do mecanismo de cursor.|  
|[CursorOptionEnum](./cursoroptionenum.md)|Especifica a funcionalidade para a qual o método de **suporte** deve ser testado.|  
|[CursorTypeEnum](./cursortypeenum.md)|Especifica o tipo de cursor usado em um objeto **Recordset** .|  
|[DataTypeEnum](./datatypeenum.md)|Especifica o tipo de dados de um **campo**, **parâmetro**ou **Propriedade**.|  
|[EditModeEnum](./editmodeenum.md)|Especifica o status de edição de um registro.|  
|[ErrorValueEnum](./errorvalueenum.md)|Especifica o tipo de erro de tempo de execução do ADO.|  
|[EventReasonEnum](./eventreasonenum.md)|Especifica o motivo que causou a ocorrência de um evento.|  
|[EventStatusEnum](./eventstatusenum.md)|Especifica o status atual da execução de um evento.|  
|[ExecuteOptionEnum](./executeoptionenum.md)|Especifica como um provedor deve executar um comando.|  
|[FieldEnum](./fieldenum.md)|Especifica os campos especiais referenciados na coleção **Fields** de um objeto **Record** .|  
|[FieldAttributeEnum](./fieldattributeenum.md)|Especifica um ou mais atributos de um objeto de **campo** .|  
|[FieldStatusEnum](./fieldstatusenum.md)|Especifica o status de um objeto de **campo** .|  
|[FilterGroupEnum](./filtergroupenum.md)|Especifica o grupo de registros a ser filtrado de um **conjunto**de registros.|  
|[GetRowsOptionEnum](./getrowsoptionenum.md)|Especifica quantos registros recuperar de um conjunto de **registros**.|  
|[IsolationLevelEnum](./isolationlevelenum.md)|Especifica o nível de isolamento de transação para um objeto de **conexão** .|  
|[LineSeparatorsEnum](./lineseparatorsenum.md)|Especifica o caractere usado como separador de linha em objetos de **fluxo** de texto.|  
|[LockTypeEnum](./locktypeenum.md)|Especifica o tipo de bloqueio colocado nos registros durante a edição.|  
|[MarshalOptionsEnum](./marshaloptionsenum.md)|Especifica quais registros devem ser retornados ao servidor.|  
|[MoveRecordOptionsEnum](./moverecordoptionsenum.md)|Especifica o comportamento do método **MoveRecord** do objeto de **registro** .|  
|[ObjectStateEnum](./objectstateenum.md)|Especifica se um objeto está aberto ou fechado, conectando-se a uma fonte de dados, executando um comando ou buscando dados.|  
|[ParameterAttributesEnum](./parameterattributesenum.md)|Especifica os atributos de um objeto de **parâmetro** .|  
|[ParameterDirectionEnum](./parameterdirectionenum.md)|Especifica se o **parâmetro** representa um parâmetro de entrada, um parâmetro de saída ou ambos, ou se o parâmetro é o valor de retorno de um procedimento armazenado.|  
|[PersistFormatEnum](./persistformatenum.md)|Especifica o formato no qual salvar um **conjunto de registros**.|  
|[PositionEnum](./positionenum.md)|Especifica a posição atual do ponteiro de registro em um **conjunto de registros**.|  
|[PropertyAttributesEnum](./propertyattributesenum.md)|Especifica os atributos de um objeto de **Propriedade** .|  
|[RecordCreateOptionsEnum](./recordcreateoptionsenum.md)|Especifica para o método de **gravação** de objeto **aberto** se um **registro** existente deve ser aberto ou se um novo **registro** deve ser criado.|  
|[RecordOpenOptionsEnum](./recordopenoptionsenum.md)|Especifica as opções para abrir um **registro**. Esses valores podem ser combinados usando um operador OR.|  
|[RecordStatusEnum](./recordstatusenum.md)|Especifica o status de um registro em relação às atualizações em lotes e outras operações em massa.|  
|[RecordTypeEnum](./recordtypeenum.md)|Especifica o tipo de objeto de **registro** .|  
|[ResyncEnum](./resyncenum.md)|Especifica se os valores subjacentes são substituídos por uma chamada para **ressincronização**.|  
|[SaveOptionsEnum](./saveoptionsenum.md)|Especifica se um arquivo deve ser criado ou substituído ao salvar de um objeto de **fluxo** . Os valores podem ser combinados com um operador AND.|  
|[SchemaEnum](./schemaenum.md)|Especifica o tipo de **conjunto de registros** de esquema que o método **OpenSchema** recupera. Especifica a direção de uma pesquisa de registro em um **conjunto de registros**.|  
|[SearchDirectionEnum](./searchdirectionenum.md)|Especifica a direção de uma pesquisa de registro em um **conjunto de registros**. Especifica o tipo de **busca** a ser executada.|  
|[SeekEnum](./seekenum.md)|Especifica o tipo de **busca** a ser executada. Especifica as opções para abrir um objeto de **fluxo** . Os valores podem ser combinados com um operador AND.|  
|[StreamOpenOptionsEnum](./streamopenoptionsenum.md)|Especifica as opções para abrir um objeto de **fluxo** . Os valores podem ser combinados com um operador AND. Especifica se o fluxo inteiro ou a próxima linha deve ser lido a partir de um objeto de **fluxo** .|  
|[StreamReadEnum](./streamreadenum.md)|Especifica se o fluxo inteiro ou a próxima linha deve ser lido a partir de um objeto de **fluxo** . Especifica o tipo de dados armazenados em um objeto de **fluxo** .|  
|[StreamTypeEnum](./streamtypeenum.md)|Especifica o tipo de dados armazenados em um objeto de **fluxo** . Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um objeto de **fluxo** .|  
|[StreamWriteEnum](./streamwriteenum.md)|Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um objeto de **fluxo** . Especifica o formato ao recuperar um **conjunto de registros** como uma cadeia de caracteres.|  
|[StringFormatEnum](./stringformatenum.md)|Especifica o formato ao recuperar um **conjunto de registros** como uma cadeia de caracteres. Especifica os atributos de transação de um objeto de **conexão** .|  
|[XactAttributeEnum](./xactattributeenum.md)|Especifica os atributos de transação de um objeto de **conexão** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](./ado-api-reference.md)   
 [Coleções ADO](./ado-collections.md)   
 [Propriedades dinâmicas do ADO](./ado-dynamic-properties.md)   
 [Apêndice B: erros do ADO](../../guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](./ado-events.md)   
 [Métodos do ADO](./ado-methods.md)   
 [Modelo de objeto ADO](./ado-object-model.md)   
 [Objetos e interfaces do ADO](./ado-objects-and-interfaces.md)   
 [Propriedades ADO](./ado-properties.md)