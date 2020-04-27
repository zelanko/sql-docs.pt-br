---
title: Definir ou alterar o método de conexão preferencial para DirectQuery | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f10d5678-d678-4251-8cce-4e30cfe15751
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9737b829a5ccab1ddc0362f2d8ac81285f0f6e1c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068695"
---
# <a name="set-or-change-the-preferred-connection-method-for-directquery"></a>Definir ou alterar o método de conexão preferencial para DirectQuery
  Quando você criar um modelo para uso em modo DirectQuery, primeiro configure o ambiente de design para oferece suporte ao uso do DirectQuery. Para fazer isso, consulte [habilitar modo de design do DirectQuery &#40;SSAS de tabela&#41;](tabular-models/enable-directquery-mode-in-ssdt.md).  
  
 Quando você estiver pronto para implantar o modelo, defina algumas propriedades adicionais para habilitar usuários a acessar seu modelo usando um dos modos do DirectQuery:  
  
-   Você precisa indicar se as consultas no modelo devem usar dados armazenados em cache ou a fonte de dados relacional. Você só pode usar um modo híbrido ou DirectQuery.  
  
-   Se você estiver usando partições, indique a partição a ser usada como a fonte de dados do DirectQuery.  
  
-   Você deve definir opções de representação para usuários que estarão acessando a fonte de dados do SQL Server.  
  
 Este procedimento descreve como definir o método de conexão preferencial para um modelo DirectQuery no designer. Ele também descreve como alterar esta propriedade no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] depois da implantação do modelo.  
  
### <a name="to-set-the-preferred-connection-method-for-a-directquery-model"></a>Para definir o método de conexão preferencial para um modelo DirectQuery  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o arquivo de solução para o modelo DirectQuery.  
  
2.  No Visual Studio, no menu **Projeto** , selecione **Propriedades**.  
  
3.  No painel **Propriedades** , altere a propriedade, **DirectQueryMode**, para um dos valores que oferecem suporte ao uso do DirectQuery:  
  
    -   **InMemory com DirectQuery**: Se você usar esta opção, o modelo será implantado mas você deverá processar o cache antes de poder executar consultas no modelo.  
  
    -   **DirectQuery com InMemory**: Se você usar esta opção, o cache estará disponível para uso por clientes se ele já tiver sido processado. Se você implantar o modelo com esta configuração e não processar o cache, alguns clientes obterão um erro ao tentar se conectar ao modelo.  
  
    -   **somente DirectQuery**: Se você usar esta opção, os metadados serão implantados mas o modelo não conterá dados. Clientes que tentam se conectar usando o modo Na memória obterão um erro, indicando que o modelo não existe ou não foi processado.  
  
4.  Se houver erros no Visual Studio, abra a **Lista de Erros** e resolva os problemas que possam impedir a implantação do modelo no modo DirectQuery.  
  
### <a name="to-verify-or-change-the-preferred-connection-method-for-a-directquery-model"></a>Para verificar ou alterar o método de conexão preferencial para um modelo DirectQuery  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], conecte-se à instância onde você implantou o modelo DirectQuery.  
  
2.  Clique com o botão direito do mouse no banco de dados modelo e selecione **Propriedades**.  
  
3.  No painel **Propriedades** , altere a propriedade **DirectQueryMode**para um destes valores:  
  
    -   **Somente DirectQuery**  
  
    -   **InMemory com DirectQuery**  
  
    -   **DirectQuery com inmemory**  
  
 Observe que estas propriedades são iguais às propriedades que você define no projeto antes da implantação no Visual Studio. Você pode alterar o modo de conexão preferencial a qualquer momento para o modo DirectQuery, desde que o modelo esteja configurado para oferecer suporte ao uso do DirectQuery.  
  
## <a name="see-also"></a>Consulte Também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Habilitar modo de design do DirectQuery &#40;SSAS de tabela&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)  
  
  
