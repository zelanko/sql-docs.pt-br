---
title: Gerenciando conexões e sessões (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statefulness [XML for Analysis]
- statelessness [XML for Analysis]
- XML for Analysis, sessions
- states [XML for Analysis]
- XMLA, sessions
- sessions [XML for Analysis]
ms.assetid: b83bb3ff-09be-4fda-9d1d-6248e04ffb21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bbd5ef006674a61830bf07de31f73c3915b0d4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62701995"
---
# <a name="managing-connections-and-sessions-xmla"></a>Gerenciando conexões e sessões (XMLA)
  A *monitoração* é uma condição durante a qual o servidor preserva a identidade e o contexto de um cliente entre chamadas de método. *Sem estado* é uma condição durante a qual o servidor não se lembra da identidade e do contexto de um cliente após a conclusão de uma chamada de método.  
  
 Para fornecer estado, XML for Analysis (XMLA) dá suporte a *sessões* que permitem que uma série de instruções seja executada juntas. Um exemplo de uma dessas séries de instruções seria a criação de um membro calculado a ser usado em consultas subsequentes.  
  
 Em geral, as sessões em XMLA seguem o comportamento a seguir, descrito pela especificação do OLE DB 2.6:  
  
-   As sessões definem o escopo do contexto de comando e de transação.  
  
-   Vários comandos podem ser executados no contexto de uma única sessão.  
  
-   O suporte para transações no contexto XMLA é por meio de comandos específicos do provedor enviados com o método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
 O XMLA define uma forma de suportar sessões em um ambiente da Web em um modo similar à abordagem usada pelo protocolo DAV (Distributed Authoring and Versioning) para a implementação do bloqueio em um ambiente flexível. Esta implementação se compara ao DAV, já que o provedor pode fazer uma sessão expirar por vários motivos (por exemplo, um tempo limite ou um erro de conexão). Quando as sessões forem suportadas, os serviços Web deverão estar atentos e prontos para lidarem com conjuntos de comandos interrompidos que deverão ser reiniciados.  
  
 A especificação do protocolo SOAP do W3C (World Wide Web Consortium) recomenda a utilização de cabeçalhos SOAP para a criação de novos protocolos sobre mensagens SOAP. A tabela a seguir lista os elementos e os atributos de cabeçalho SOAP definidos pelo XMLA para iniciar, manter e fechar uma sessão.  
  
|Cabeçalho SOAP|Descrição|  
|-----------------|-----------------|  
|BeginSession|Este cabeçalho solicita que o provedor crie uma sessão nova. O provedor deve responder criando uma sessão nova e retornando a ID de sessão como parte do cabeçalho Session na resposta SOAP.|  
|SessionId|A área de valor contém a ID de sessão que deve ser usada em cada chamada de método para o resto da sessão. O provedor na resposta de SOAP envia esta marca e o cliente também deve enviar este atributo com cada elemento do cabeçalho Session.|  
|Session|Para cada chamada de método ocorrida na sessão, este cabeçalho deverá ser usado e a ID de sessão deverá ser incluída na área de valor do cabeçalho.|  
|EndSession|Para finalizar a sessão, use este cabeçalho. A ID de sessão deve ser incluída com a área de valor.|  
  
> [!NOTE]  
>  A ID de sessão não garante que uma sessão permanecerá válida. Se a sessão expirar (por exemplo, se o tempo limite for alcançado ou se a conexão for interrompida), o provedor poderá optar por encerrar e reverter as ações dessa sessão. Como resultado, todas as chamadas de método subsequentes feitas do cliente em uma ID de sessão falharão com um erro que indicará uma sessão inválida. Um cliente deve lidar com esta condição e estar preparado para reenviar as chamadas de método de sessão desde o princípio.  
  
## <a name="legacy-code-example"></a>Exemplo de código herdado  
 O exemplo a seguir mostra como as sessões são suportadas.  
  
1.  Para iniciar a sessão, acrescente um cabeçalho BeginSession em SOAP à chamada de método XMLA a partir do cliente. Inicialmente, a área de valor estará em branco, já que a ID de sessão ainda não é conhecida.  
  
    ```  
    <SOAP-ENV:Envelope  
       xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
       SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
       <SOAP-ENV:Header>  
          <XA:BeginSession  
             xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
             xsi:type="xsd:int"  
             mustUnderstand="1"/>  
       </SOAP-ENV:Header>  
       <SOAP-ENV:Body>  
          ...<!-- Discover or Execute call goes here.-->  
       </SOAP-ENV:Body>  
    </SOAP-ENV:Envelope>  
    ```  
  
2.  A mensagem de resposta SOAP do provedor inclui a ID de sessão na área de cabeçalho de retorno, usando a marca \<de cabeçalho XMLA> SessionID.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
3.  O cabeçalho Session deve ser adicionado a cada chamada de método da sessão, com a ID de sessão retornada do provedor.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
4.  Quando a sessão for concluída, a \<marca de> de EndSession será usada, contendo o valor de ID de sessão relacionado.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:EndSession  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          xsi:type="xsd:int"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
