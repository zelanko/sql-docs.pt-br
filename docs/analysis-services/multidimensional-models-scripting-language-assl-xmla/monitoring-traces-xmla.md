---
title: Monitorando rastreamentos (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d63e2b7e07c01d0f937618cfc521921e9d16dc43
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="monitoring-traces-xmla"></a>Monitorando rastreamentos (XMLA)
  Você pode usar o [assinar](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) do XML for Analysis (XMLA) para monitorar um rastreamento existente definido em uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. O **assinar** comando retorna os resultados de um rastreamento como um conjunto de linhas.  
  
## <a name="specifying-a-trace"></a>Especificando um rastreamento  
 O [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade do **assinar** comando deve conter uma referência de objeto para um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância ou um rastreamento em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. Se o **objeto** propriedade não for especificada, ou um identificador de rastreamento não está especificado no **objeto** propriedade, o **assinar** comando monitora o rastreamento de sessão padrão para a sessão explícita especificada no cabeçalho SOAP para o comando.  
  
## <a name="returning-results"></a>Retornando resultados  
 O **assinar** comando retorna um conjunto de linhas que contêm os eventos de rastreamento capturados pelo rastreamento especificado. O **assinar** comando retorna os resultados do rastreamento até que o comando é cancelado, o [Cancelar](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md) comando.  
  
 O conjunto de linhas contém as colunas listadas na tabela a seguir.  
  
|Coluna|Data type|Description|  
|------------|---------------|-----------------|  
|EventClass|Integer|A classe de evento do evento recebido pelo rastreamento.|  
|EventSubclass|Long integer|A subclasse do evento recebido pelo rastreamento.|  
|CurrentTime|Datetime|O horário no qual o evento foi iniciado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|Datetime|O horário no qual o evento foi iniciado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|Datetime|O horário de término evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.<br /><br /> Esta coluna não é preenchida para classes de evento que descrevem o início de um processo ou de uma ação.|  
|Duration|Long integer|O tempo total (em milissegundos) decorrido no evento.|  
|CPUTime|Long integer|O tempo de processador (em milissegundos) decorrido no evento.|  
|JobID|Long integer|O identificador de trabalho para o processo.|  
|SessionID|Cadeia de caracteres|O identificador da sessão para a qual o evento ocorreu.|  
|SessionType|Cadeia de caracteres|O tipo da sessão para a qual o evento ocorreu.|  
|ProgressTotal|Long integer|O número total ou a quantidade de progresso informados pelo evento.|  
|IntegerData|Long integer|Dados inteiros associados ao evento. O conteúdo desta coluna depende da classe de evento e da subclasse do evento.|  
|ObjectID|Cadeia de caracteres|O identificador do objeto para o qual o evento ocorreu.|  
|ObjectType|Cadeia de caracteres|O tipo do objeto especificado em ObjectName.|  
|ObjectName|Cadeia de caracteres|O nome do objeto para o qual o evento ocorreu.|  
|ObjectPath|Cadeia de caracteres|O caminho hierárquico do objeto para o qual o evento ocorreu. O caminho é representado como uma cadeia de caracteres delimitada por vírgulas de identificadores de objetos para os pais do objeto especificado em ObjectName.|  
|ObjectReference|Cadeia de caracteres|A representação XML da referência de objeto para o objeto especificado em ObjectName.|  
|NestLevel|Integer|O nível da transação para a qual o evento ocorreu.|  
|NumSegments|Long integer|O número de segmentos de dados afetados ou acessados pelo comando para o qual o evento ocorreu.|  
|Severity|Integer|O nível de severidade de uma exceção para o evento. A coluna pode conter um dos seguintes valores:<br /><br /> <br /><br /> 0: êxito<br /><br /> <br /><br /> 1: obter informações<br /><br /> <br /><br /> 2: aviso<br /><br /> <br /><br /> 3: erro|  
|Success|Booliano|Indica se um comando teve êxito ou se falhou.|  
|Erro|Long integer|O número do erro do evento, se aplicável.|  
|ConnectionID|Cadeia de caracteres|O identificador da conexão para a qual o evento ocorreu.|  
|DatabaseName|Cadeia de caracteres|O nome do banco de dados para o qual o evento ocorreu.|  
|NTUserName|Cadeia de caracteres|O nome de usuário do Windows associado ao evento.|  
|NTDomainName|Cadeia de caracteres|O domínio do Windows do usuário associado ao evento.|  
|ClientHostName|Cadeia de caracteres|O nome do computador em que o aplicativo cliente está sendo executado. Essa coluna é preenchida com os valores passados pelo aplicativo cliente.|  
|ClientProcessID|Long integer|O identificador de processo do aplicativo cliente.|  
|ApplicationName|Cadeia de caracteres|O nome do aplicativo cliente que criou a conexão com a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa coluna é preenchida com os valores passados pelo aplicativo cliente e não com o nome exibido do programa.|  
|NTCanonicalUserName|Cadeia de caracteres|O nome de usuário canônico do Windows associado ao evento.|  
|SPID|Cadeia de caracteres|A SPID (ID de processo do servidor) da sessão para a qual o evento ocorreu. O valor dessa coluna corresponde diretamente à ID de sessão especificada no cabeçalho SOAP da mensagem XMLA para a qual o evento ocorreu.|  
|TextData|Cadeia de caracteres|Os dados de texto associados ao evento. O conteúdo desta coluna depende da classe de evento e da subclasse do evento.|  
|ServerName|Cadeia de caracteres|O nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para a qual o evento ocorreu.|  
|RequestParameters|Cadeia de caracteres|Os parâmetros da consulta parametrizada ou do comando XMLA para os quais o evento ocorreu.|  
|RequestProperties|Cadeia de caracteres|As propriedades do método XMLA para o qual o evento ocorreu.|  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

