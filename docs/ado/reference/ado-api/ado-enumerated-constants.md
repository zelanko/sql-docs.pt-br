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
ms.openlocfilehash: 7d126d0783e448dab786a228b4e10a8ec7c0f840
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451438"
---
# <a name="ado-enumerated-constants"></a>Constantes enumeradas do ADO
Para auxiliar na depuração, as enumerações do ADO listam um valor para cada constante. No entanto, esse valor é puramente consultivo e pode ser alterado de uma versão do ADO para outra. Seu código só deve depender do nome, não do valor real, de cada constante enumerada.  
  
|Constante|DESCRIÇÃO|  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Para um objeto de **conjunto de registros** do RDS, especifica a prioridade de execução do thread assíncrono que recupera dados.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Especifica quando o provedor **MSDataShape** recalcula as colunas agregadas e calculadas em um **conjunto de registros**hierárquico.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um objeto **Recordset** .|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Especifica se o método **UpdateBatch** é seguido por uma operação de método de **ressincronização** implícita e, nesse caso, o escopo dessa operação.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Especifica quais registros são afetados por uma operação.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Especifica um indicador que indica onde a operação deve começar.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Especifica como um argumento de comando deve ser interpretado.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Especifica a posição relativa de dois registros representados por seus indicadores.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Especifica as permissões disponíveis para modificar dados em uma **conexão**, abrir um **registro**ou especificar valores para a propriedade **Mode** dos objetos **Record** e **Stream** .|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Especifica se o método **Open** de um objeto de **conexão** deve retornar após (sincronamente) ou antes (assincronamente) que a conexão seja estabelecida.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Especifica se uma caixa de diálogo deve ser exibida para solicitar parâmetros ausentes ao abrir uma conexão com uma fonte de dados ODBC.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Especifica o comportamento do método **CopyRecord** .|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Especifica o local do mecanismo de cursor.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Especifica a funcionalidade para a qual o método de **suporte** deve ser testado.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Especifica o tipo de cursor usado em um objeto **Recordset** .|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Especifica o tipo de dados de um **campo**, **parâmetro**ou **Propriedade**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Especifica o status de edição de um registro.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Especifica o tipo de erro de tempo de execução do ADO.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Especifica o motivo que causou a ocorrência de um evento.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Especifica o status atual da execução de um evento.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Especifica como um provedor deve executar um comando.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Especifica os campos especiais referenciados na coleção **Fields** de um objeto **Record** .|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Especifica um ou mais atributos de um objeto de **campo** .|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Especifica o status de um objeto de **campo** .|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Especifica o grupo de registros a ser filtrado de um **conjunto**de registros.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Especifica quantos registros recuperar de um conjunto de **registros**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Especifica o nível de isolamento de transação para um objeto de **conexão** .|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Especifica o caractere usado como separador de linha em objetos de **fluxo** de texto.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Especifica o tipo de bloqueio colocado nos registros durante a edição.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Especifica quais registros devem ser retornados ao servidor.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Especifica o comportamento do método **MoveRecord** do objeto de **registro** .|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Especifica se um objeto está aberto ou fechado, conectando-se a uma fonte de dados, executando um comando ou buscando dados.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Especifica os atributos de um objeto de **parâmetro** .|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Especifica se o **parâmetro** representa um parâmetro de entrada, um parâmetro de saída ou ambos, ou se o parâmetro é o valor de retorno de um procedimento armazenado.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Especifica o formato no qual salvar um **conjunto de registros**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Especifica a posição atual do ponteiro de registro em um **conjunto de registros**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Especifica os atributos de um objeto de **Propriedade** .|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Especifica para o método de **gravação** de objeto **aberto** se um **registro** existente deve ser aberto ou se um novo **registro** deve ser criado.|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Especifica as opções para abrir um **registro**. Esses valores podem ser combinados usando um operador OR.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Especifica o status de um registro em relação às atualizações em lotes e outras operações em massa.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Especifica o tipo de objeto de **registro** .|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Especifica se os valores subjacentes são substituídos por uma chamada para **ressincronização**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Especifica se um arquivo deve ser criado ou substituído ao salvar de um objeto de **fluxo** . Os valores podem ser combinados com um operador AND.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Especifica o tipo de **conjunto de registros** de esquema que o método **OpenSchema** recupera. Especifica a direção de uma pesquisa de registro em um **conjunto de registros**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Especifica a direção de uma pesquisa de registro em um **conjunto de registros**. Especifica o tipo de **busca** a ser executada.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Especifica o tipo de **busca** a ser executada. Especifica as opções para abrir um objeto de **fluxo** . Os valores podem ser combinados com um operador AND.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Especifica as opções para abrir um objeto de **fluxo** . Os valores podem ser combinados com um operador AND. Especifica se o fluxo inteiro ou a próxima linha deve ser lido a partir de um objeto de **fluxo** .|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Especifica se o fluxo inteiro ou a próxima linha deve ser lido a partir de um objeto de **fluxo** . Especifica o tipo de dados armazenados em um objeto de **fluxo** .|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Especifica o tipo de dados armazenados em um objeto de **fluxo** . Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um objeto de **fluxo** .|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Especifica se um separador de linha é acrescentado à cadeia de caracteres gravada em um objeto de **fluxo** . Especifica o formato ao recuperar um **conjunto de registros** como uma cadeia de caracteres.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Especifica o formato ao recuperar um **conjunto de registros** como uma cadeia de caracteres. Especifica os atributos de transação de um objeto de **conexão** .|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Especifica os atributos de transação de um objeto de **conexão** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Coleções ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Apêndice B: erros do ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos do ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objeto ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces do ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propriedades ADO](../../../ado/reference/ado-api/ado-properties.md)
