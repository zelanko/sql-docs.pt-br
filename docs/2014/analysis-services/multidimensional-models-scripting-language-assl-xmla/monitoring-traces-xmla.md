---
title: Monitoramento de rastreamentos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
author: minewiskan
ms.author: owend
ms.openlocfilehash: a2ca181b7c194fdd3909875f881d1030a77ae039
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544898"
---
# <a name="monitoring-traces-xmla"></a>Monitorando rastreamentos (XMLA)
  Você pode usar o comando [Subscribe](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) no XML for Analysis (XMLA) para monitorar um rastreamento existente definido em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O comando `Subscribe` retorna os resultados de um rastreamento como um conjunto de linhas.  
  
## <a name="specifying-a-trace"></a>Especificando um rastreamento  
 A propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `Subscribe` comando deve conter uma referência de objeto para uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância ou um rastreamento em uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. Se a propriedade `Object` não for especificada, ou se o identificador do rastreamento não for especificado na propriedade `Object`, o comando `Subscribe` vai monitorar o rastreamento padrão de sessão para a sessão explícita especificada no cabeçalho SOAP do comando.  
  
## <a name="returning-results"></a>Retornando resultados  
 O comando `Subscribe` retorna um conjunto de linhas que contém os eventos de rastreamento capturados pelo rastreamento especificado. O `Subscribe` comando retorna os resultados de rastreamento até que o comando seja cancelado pelo comando [Cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) .  
  
 O conjunto de linhas contém as colunas listadas na tabela a seguir.  
  
|Coluna|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|EventClass|Inteiro|A classe de evento do evento recebido pelo rastreamento.|  
|EventSubclass|Long integer|A subclasse do evento recebido pelo rastreamento.|  
|CurrentTime|Datetime|O horário no qual o evento foi iniciado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|Datetime|O horário no qual o evento foi iniciado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|Datetime|O horário de término evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.<br /><br /> Esta coluna não é preenchida para classes de evento que descrevem o início de um processo ou de uma ação.|  
|Duration|Long integer|O tempo total (em milissegundos) decorrido no evento.|  
|CPUTime|Long integer|O tempo de processador (em milissegundos) decorrido no evento.|  
|JobID|Long integer|O identificador de trabalho para o processo.|  
|SessionID|String|O identificador da sessão para a qual o evento ocorreu.|  
|SessionType|String|O tipo da sessão para a qual o evento ocorreu.|  
|ProgressTotal|Long integer|O número total ou a quantidade de progresso informados pelo evento.|  
|IntegerData|Long integer|Dados inteiros associados ao evento. O conteúdo desta coluna depende da classe de evento e da subclasse do evento.|  
|ObjectID|String|O identificador do objeto para o qual o evento ocorreu.|  
|ObjectType|String|O tipo do objeto especificado em ObjectName.|  
|ObjectName|String|O nome do objeto para o qual o evento ocorreu.|  
|ObjectPath|String|O caminho hierárquico do objeto para o qual o evento ocorreu. O caminho é representado como uma cadeia de caracteres delimitada por vírgulas de identificadores de objetos para os pais do objeto especificado em ObjectName.|  
|ObjectReference|String|A representação XML da referência de objeto para o objeto especificado em ObjectName.|  
|NestLevel|Inteiro|O nível da transação para a qual o evento ocorreu.|  
|NumSegments|Long integer|O número de segmentos de dados afetados ou acessados pelo comando para o qual o evento ocorreu.|  
|Severity|Inteiro|O nível de severidade de uma exceção para o evento. A coluna pode conter um dos seguintes valores:<br /><br /> Valor: 0 = êxito<br /><br /> Valor: 1 = informações<br /><br /> Valor: 2 = aviso<br /><br /> Valor: 3 = erro|  
|Êxito|Booliano|Indica se um comando teve êxito ou se falhou.|  
|Erro|Long integer|O número do erro do evento, se aplicável.|  
|ConnectionID|String|O identificador da conexão para a qual o evento ocorreu.|  
|DatabaseName|String|O nome do banco de dados para o qual o evento ocorreu.|  
|NTUserName|String|O nome de usuário do Windows associado ao evento.|  
|NTDomainName|String|O domínio do Windows do usuário associado ao evento.|  
|ClientHostName|String|O nome do computador em que o aplicativo cliente está sendo executado. Essa coluna é preenchida com os valores passados pelo aplicativo cliente.|  
|ClientProcessID|Long integer|O identificador de processo do aplicativo cliente.|  
|ApplicationName|String|O nome do aplicativo cliente que criou a conexão com a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa coluna é preenchida com os valores passados pelo aplicativo cliente e não com o nome exibido do programa.|  
|NTCanonicalUserName|String|O nome de usuário canônico do Windows associado ao evento.|  
|SPID|String|A SPID (ID de processo do servidor) da sessão para a qual o evento ocorreu. O valor dessa coluna corresponde diretamente à ID de sessão especificada no cabeçalho SOAP da mensagem XMLA para a qual o evento ocorreu.|  
|TextData|String|Os dados de texto associados ao evento. O conteúdo desta coluna depende da classe de evento e da subclasse do evento.|  
|ServerName|String|O nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para a qual o evento ocorreu.|  
|RequestParameters|String|Os parâmetros da consulta parametrizada ou do comando XMLA para os quais o evento ocorreu.|  
|RequestProperties|String|As propriedades do método XMLA para o qual o evento ocorreu.|  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
