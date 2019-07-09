---
title: Desconectar usuários e sessões no Analysis Services Server | Microsoft Docs
ms.date: 07/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 696c6548dadda2412566acf7fae1e2cff2b28095
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624394"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Desconectar usuários e sessões no Analysis Services Server
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  Como administrador, você talvez queira atividade do usuário final como parte do gerenciamento de carga de trabalho. Para fazer isso, cancele sessões e conexões. As sessões podem ser formadas automaticamente quando uma consulta é executada (implícito) ou nomeada no momento da criação pelo administrador (explícito). As conexões são canais abertos nos quais as consultas podem ser executadas. Tanto as sessões quanto as conexões podem ser encerradas enquanto estiverem ativas. Por exemplo, você talvez queira encerrar o processamento de uma sessão se o processamento estiver demorando muito ou se surgir alguma dúvida sobre se o comando que está sendo executado foi escrito corretamente.  
  
## <a name="ending-sessions-and-connections"></a>Encerrando sessões e conexões  
 Para gerenciar sessões e conexões, use as exibições de gerenciamento dinâmico (DMVs) e XMLA:  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do Analysis Services.  
  
2.  Cole qualquer uma das consultas de DMV a seguir em uma janela de consulta MDX para obter uma lista de todas as sessões, conexões e comandos que estão sendo executados no momento:  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  (Esta consulta não se aplica ao Azure Analysis Services)
  
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

Cancelar um SPID/SessionID cancelará quaisquer comandos ativos em execução na sessão correspondente ao SPID/SessionID. Cancelar uma conexão identificará a sessão associada a conexão e cancelar os comandos de Active Directory em execução naquela sessão. Em casos raros, uma conexão não for fechada se o mecanismo não é possível controlar todas as sessões e os SPIDs associados com a conexão; Por exemplo, quando várias sessões estão abertas em um cenário HTTP.   
  
Para saber mais sobre o XMLA referenciado neste tópico, consulte [executar método &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) e [Cancelar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conexões e sessões &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [Elemento BeginSession &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [Elemento EndSession &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Elemento Session &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
