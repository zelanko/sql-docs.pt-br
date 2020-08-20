---
description: 'Lição 1-8: Anotar e formatar o pacote da Lição 1'
title: 'Etapa 8: Anotar e formatar o pacote da Lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 08e5668fcdc3fe41e54965b01db9325c861fa98f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462018"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>Lição 1-8: Anotar e formatar o pacote da Lição 1 

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Agora que você concluiu a configuração do pacote da Lição 1, é uma boa hora para organizar o layout do pacote. Se as formas em layouts de fluxo de controle e de dados forem de tamanhos diferentes ou não estiverem dispostas uniformemente, poderá ser mais difícil entender o pacote.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools fornece ferramentas para formatar facilmente o layout do pacote. Os recursos de formatação incluem a capacidade de criar formas do mesmo tamanho, alinhar formas e alterar o espaçamento horizontal e vertical entre os espaçamentos.  
  
Outro modo para melhorar a compreensão de funcionalidade de pacote é adicionar anotações que descrevem a funcionalidade do pacote.  
  
Nesta tarefa, você usa os recursos de formatação nas ferramentas de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para melhorar o layout do fluxo de dados e também adicionar uma anotação.  
  
## <a name="format-the-layout-of-the-data-flow"></a>Formatar o layout do fluxo de dados  
  
1.  Se o pacote da Lição 1 ainda não estiver aberto, clique duas vezes em **Lição 1.dtsx** no **Gerenciador de Soluções**.  
  
2.  Selecione a guia **Fluxo de Dados**.  
  
3.  Para selecionar todos os componentes de fluxo de dados ao mesmo tempo, use **Editar** > **Selecionar Tudo**.
  
4.  No menu **Formato**, selecione **Igualar Tamanho** e, em seguida, selecione **Ambos**.  
  
5.  Com os objetos de fluxo de dados selecionados, no menu **Formato**, selecione **Alinhar** e, em seguida, **Centros**.  

6.  Com os objetos de fluxo de dados selecionados, no menu **Formato**, aponte para **Espaçamento Vertical** e, em seguida, selecione **Igualar**.  
  
## <a name="add-an-annotation-to-the-data-flow"></a>Adicionar uma anotação ao fluxo de dados  
  
1.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de dados e selecione **Adicionar Anotação**.  
  
2.  Insira ou cole o texto a seguir na caixa de anotação.  
  
    O fluxo de dados extrai os dados de um arquivo, pesquisa valores na coluna CurrencyKey da tabela DimCurrency e na coluna DateKey da tabela DimDate, além de gravar os dados na tabela NewFactCurrencyRate.
  
    Para encapsular o texto na caixa de anotação, posicione o cursor no local em que deseja começar uma nova linha e pressione **Enter**.  
  
    Se você não adicionar texto à caixa de anotação, essa caixa desaparecerá quando você clicar fora dela.  Devido a esse comportamento, caso você deseje colar o texto na caixa de anotação, copie o texto para a área de transferência antes de selecionar Adicionar Anotação. 
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 9: Testar o pacote da Lição 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
