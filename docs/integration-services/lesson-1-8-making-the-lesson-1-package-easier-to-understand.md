---
title: "Etapa 8: Tornando o pacote da lição 1 mais fácil de entender | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 55bd386054f3a7d066dc8c28c13e22ae82e9f0cb
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-8---making-the-lesson-1-package-easier-to-understand"></a>Lição 1-8-tornando o pacote da lição 1 mais fácil de compreender
Agora que você concluiu a configuração do pacote da Lição 1, é uma boa ideia verificar o layout do pacote. Se as formas dos layouts de controle e dos fluxos de dados são de tamanhos aleatórias ou se as formas não estão alinhadas ou agrupadas, a funcionalidade de pacote pode ser mais difícil de ser entendida.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecem recursos que facilitam e agilizam a formatação do layout do pacote. Os recursos de formatação incluem a capacidade de criar formas do mesmo tamanho, alinhar formas e manipular o espaçamento horizontal e vertical entre os espaçamentos.  
  
Outro modo para melhorar a compreensão de funcionalidade de pacote é adicionar anotações que descrevem a funcionalidade do pacote.  
  
Nesta tarefa, você utilizará os recursos de formatação nas ferramentas de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para melhorar o layout do fluxo de dados e também adicionar uma anotação ao fluxo de dados.  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>Para formatar o layout do fluxo de dados  
  
1.  Se o pacote da Lição 1 ainda não estiver aberto, no Gerenciador de Soluções, clique duas vezes em Lição 1.dtsx.  
  
2.  Clique na guia **Fluxo de Dados** .  
  
3.  Posicione o cursor na parte superior e à direita da transformação Extrair Moeda de Exemplo e clique e arraste o cursor por todos os componentes do fluxo de dados.  
  
4.  No menu **Formatar** , aponte para **Igualar Tamanho**e clique em **Ambos**.  
  
5.  Com os objetos de fluxo de dados selecionados, no menu **Formatar** , aponte para **Alinhar**e clique em **À esquerda**.  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>Para adicionar uma anotação ao fluxo de dados  
  
1.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de dados e clique em **Adicionar Anotação**.  
  
2.  Digite ou cole o texto a seguir na caixa de anotação.  
  
    **O fluxo de dados extrai os dados de um arquivo, pesquisa valores na coluna CurrencyKey da tabela DimCurrency e na coluna DateKey da tabela DimDate, além de gravar os dados na tabela NewFactCurrencyRate.**  
  
    Para usar a quebra de linhas no texto da caixa de anotação, posicione o cursor no local em que deseja começar uma nova linha e pressione a tecla Enter.  
  
    Se você não inserir um texto na caixa de anotação, essa caixa desaparecerá ao clicar fora dela.  
  
## <a name="next-steps"></a>Próximas etapas  
[Etapa 9: Testando o pacote de tutorial da Lição 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  

