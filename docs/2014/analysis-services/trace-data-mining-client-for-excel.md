---
title: Rastreamento (cliente de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tracer
- connections
ms.assetid: 4aea3e17-cd0f-48dd-8f22-b54a6c716426
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 576cb395f7f488eec8ebf28ab5bc7f226cb81809
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065890"
---
# <a name="trace-data-mining-client-for-excel"></a>Rastrear (Cliente de Mineração de Dados para Excel)
  ![Botão de rastreamento](media/misc-trace.gif "botão de rastreamento")  
  
 A caixa de diálogo **Rastreamento** ajuda a monitorar as instruções enviadas à instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você está usando para mineração de dados. Depois que você criar uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], todas as interações entre o cliente e o servidor serão registradas no painel **Rastreamento** , incluindo instruções que criam estruturas, adicionam modelos de mineração e fazem previsões, além de algumas mensagens retornadas do servidor.  
  
 Dependendo da ação solicitada, a instrução talvez seja uma consulta de definição de dados DMX ou uma consulta de manipulação de dados, um pacote ASSL do Analysis Services ou uma chamada a um procedimento armazenado do Analysis Services. No entanto, os resultados numéricos e os valores de dados reais não são mostrados.  
  
 **Rastrear** monitora apenas a conexão atual. O conteúdo da caixa de diálogo **Rastreamento** não é armazenado.  
  
## <a name="options"></a>Opções  
 Painel Rastreamento  
 Lista todas as instruções enviadas do cliente do Excel ao servidor.  
  
 Dependendo da ação solicitada, talvez a instrução seja uma manipulação de dados DMX ou uma instrução de definição de dados, uma chamada a um procedimento armazenado do Analysis Services ou um pacote XML/A.  
  
 **Conexão atual**  
 Clique para exibir a definição da conexão atual. A definição inclui o nome da conexão, o provedor, a fonte de dados e o catálogo, a hora do último uso da conexão para uma transação e o estado atual (Aberta, Inativa).  
  
 **Usar modelos de sessão**  
 Marque esta caixa de seleção para armazenar modelos e estruturas de mineração de dados como objetos temporários no servidor. As estruturas e os modelos criados ficarão disponíveis apenas durante a sessão atual.  
  
 Desmarque esta opção para salvar as estruturas ou os modelos armazenando-os no servidor Analysis Services.  
  
 **Observação** A capacidade de usar objetos temporários está disponível somente quando você está utilizando as Ferramentas de Análise de Tabela para Excel. Os modelos de Mineração de Dados do Visio e o Cliente de Mineração de Dados para Excel requerem o armazenamento de estruturas e modelos no servidor.  
  
## <a name="tracing-temporary-structures-and-models"></a>Rastreando estruturas e modelos temporários  
 Se você estiver usando as Ferramentas de Análise de Tabela, que por padrão criam estruturas e modelos temporários, a atividade entre o servidor e o cliente será monitorada, mas as estruturas ou os modelos criados não serão salvos permanentemente no servidor.  
  
 Para preservar seu trabalho ao usar uma das Ferramentas de Análise de Tabela, desmarque a opção **Usar modelos de sessão**, para fazer com que os modelos sejam salvos permanentemente no servidor. Também é possível copiar as instruções no painel **Rastreamento** em um arquivo, para que você possa recriar seu trabalho depois.  
  
## <a name="understanding-sessions"></a>Entendendo sessões  
 Quando você se conecta a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o suplemento de mineração de dados inicia uma sessão. Cada sessão recebe um identificador que identifica uma sessão existente na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . No entanto, um identificador de sessão não garante que uma sessão permaneça válida. A sessão poderá expirar se seu tempo limite for alcançado ou se a conexão associada a ela for interrompida. Se a sessão expirar e não for mais válida, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] finalizará a sessão e reverterá as transações que estiverem sendo processadas. Se uma mensagem for enviada com um identificador de sessão que não for mais válido, ocorrerá falha na mensagem com um erro indicando que não é possível encontrar a sessão especificada.  
  
 Embora alguns modelos de mineração de dados sejam armazenados explicitamente no servidor, isso não acontece com os modelos e as estruturas de mineração de sessão; além disso, nenhum registro persiste da atividade de mineração de dados de sessão. Como as estruturas e os modelos temporários de mineração são excluídos assim que você encerra a sessão, evite fechar a pasta de trabalho do Excel antes de salvar qualquer trabalho que você queira manter.  
  
## <a name="changing-connections"></a>Alterando conexões  
 A alteração de conexões não exclui rastreamentos de conexões anteriores. Somente o fechamento da pasta de trabalho apaga a sessão.  
  
 Se você alterar conexões ao trabalhar em uma pasta de trabalho do Excel, a alteração de conexões não será registrada no painel **Rastreamento** . Para exibir explicitamente o nome e o status da conexão atual, você deve clicar em **Conexão Atual**.  
  
## <a name="understanding-statements-in-the-tracer"></a>Compreendendo as instruções no rastreamento  
 DMX é uma linguagem que você pode usar para criar e trabalhar com modelos de mineração de dados no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. É possível usar DMX para criar a estrutura de novos modelos de mineração de dados, treinar esses modelos e pesquisar, gerenciar e fazer previsões sobre eles. A extensão DMX é composta de instruções DLL (linguagem de definição de dados), instruções DML (linguagem de manipulação de dados), funções e operadores.  
  
 Uma análise completa das instruções DMX e sua sintaxe está além do escopo deste tópico. No entanto, você pode usar as informações no painel **Rastreamento** para obter detalhes sobre o comportamento de uma instrução DMX. Os Suplementos de Mineração de Dados para Excel também podem ajudá-lo a criar instruções DMX complexas e a interagir com um servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [consulta &#40;SQL Server Data Mining Add-ins&#41;](query-sql-server-data-mining-add-ins.md).  
  
> [!NOTE]  
>  Muitas instruções DMX são parametrizadas. Para tipos simples, os valores dos parâmetros são listados na instrução. Entretanto, para tipos complexos, apenas o tipo do parâmetro é listado.  
  
 O SQL Server Analysis Services também usa o protocolo XMLA (XML for Analysis) para manipular todas as comunicações entre aplicativos cliente, inclusive o Cliente de Mineração de Dados para Excel e uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obter mais informações sobre a sintaxe DMX e os comandos e elementos no XMLA, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Algumas das instruções enviadas ao servidor podem incluir consultas que chamam procedimentos armazenados do sistema do Analysis Services. Para obter mais informações, consulte os Manuais Online do SQL Server.  
  
  
