---
title: "Desconectar usuários e sessões no Analysis Services Server | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ending user activity [Analysis Services]
- connections [Analysis Services]
- sessions [Analysis Services]
ms.assetid: 3b0145a2-f21d-4dd0-a09e-83afeb2ff4a9
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb53b656c14090ada93184d8453ad79ab1ff706c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Desconectar usuários e sessões no Analysis Services Server
  Um administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] talvez queira encerrar a atividade de usuário como parte do gerenciamento da carga de trabalho. Para fazer isso, cancele sessões e conexões. As sessões podem ser formadas automaticamente quando uma consulta é executada (implícito) ou nomeada no momento da criação pelo administrador (explícito). As conexões são canais abertos nos quais as consultas podem ser executadas. Tanto as sessões quanto as conexões podem ser encerradas enquanto estiverem ativas. Por exemplo, o administrador pode encerrar o processamento de uma sessão caso o processamento esteja demorando muito ou se surgir alguma dúvida sobre a gravação do comando que está sendo executado.  
  
## <a name="ending-sessions-and-connections"></a>Encerrando sessões e conexões  
 Para gerenciar sessões e conexões, você pode usar DMVs (Exibições de gerenciamento dinâmico) e XMLA:  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do Analysis Services.  
  
2.  Cole qualquer uma das consultas de DMV a seguir em uma janela de consulta MDX para obter uma lista de todas as sessões, conexões e comandos que estão sendo executados no momento:  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  
  
     `Select * from $System.Discover_Commands`  
  
3.  Pressione F5 para executar a consulta.  
  
     A consulta DMV retorna informações da sessão e da conexão em um conjunto de resultados de tabela que é mais fácil de ler e copiar.  
  
 Mantenha a janela de consulta aberta. Na próxima etapa, você desejará retornar a esta página para copiar os SPIDs da sessão que deseja desconectar.  
  
 Para encerrar uma sessão, abra uma segunda janela de consulta XMLA.  
  
1.  Cole a sintaxe a seguir em uma janela de consulta MDX, substituindo o espaço reservado de ConnectionID, SessionID ou SPID por um valor válido copiado da etapa anterior.  
  
    ```  
    <Cancel xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  Pressione F5 para executar o comando cancelar.  
  
 O encerramento de uma conexão cancela todas as sessões e os SPIDs, fechando a sessão de host.  
  
 O encerramento de uma sessão interrompe todos os comandos (SPIDs) que estão sendo executados como parte da sessão em questão.  
  
 O encerramento de um SPID cancela um comando específico.  
  
 Em casos raros, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não fechará uma conexão se não puder acompanhar todas as sessões e os SPIDs associados à conexão (por exemplo, quando várias sessões estiverem abertas em um cenário HTTP).  
  
 Para obter mais informações sobre o XMLA referenciado neste tópico, consulte [Executar método &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md) e [Elemento Cancel &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Elemento BeginSession &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [Elemento EndSession &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Elemento Session &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)  
  
  

