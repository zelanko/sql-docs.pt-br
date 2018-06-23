---
title: Criar um cubo usando o Assistente de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], creating
ms.assetid: d46d659c-3a4e-4364-94ac-f5eb6ba0ec25
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b876ddfc76414b45f090f575ce93c5937fe2e05b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115535"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>Criar um cubo usando o Assistente para Cubos
  Você pode criar um novo cubo usando o Assistente para Cubos do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-cube"></a>Para criar um novo cubo  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Cubos**e clique em **Novo Cubo**.  
  
2.  Na página **Selecionar Método de Criação** do Assistente para Cubos, selecione **Usar tabelas existentes**e clique em **Avançar**.  
  
    > [!NOTE]  
    >  Ocasionalmente pode ser necessário criar um cubo sem usar as tabelas existentes. Para criar um cubo vazio, selecione **Criar um cubo vazio**. Para gerar tabelas, selecione **Gerar tabelas na fonte de dados**.  
  
3.  Na página **Selecionar Tabelas de Grupos de Medidas** , execute os seguintes procedimentos:  
  
    1.  Na lista **Exibição da fonte de dados** , selecione uma exibição da fonte de dados.  
  
    2.  Na lista **Tabelas de grupos de medidas** , selecione as tabelas que serão usadas para criar grupos de medidas.  
  
    3.  Clique em **Avançar**.  
  
4.  Na página **Selecionar Medidas** , selecione as medidas que você quer incluir no cubo e clique em **Avançar**.  
  
     Opcionalmente, você pode alterar os nomes das medidas e grupos de medidas.  
  
5.  Na página **Selecionar Dimensões Existentes** , selecione as dimensões existentes a serem incluídas no cubo e, em seguida, clique em **Avançar**.  
  
    > [!NOTE]  
    >  A página **Selecionar Dimensões Existentes** será exibida se existirem dimensões no banco de dados para qualquer um dos grupos de medidas selecionados.  
  
6.  Na página **Selecionar Novas Dimensões** , selecione as dimensões novas para criar e depois clique em **Avançar**.  
  
    > [!NOTE]  
    >  A página **Selecionar Novas Dimensões** será exibida se alguma tabela for boa candidata para a tabela de dimensão e se as tabelas ainda não tiverem sido usadas pelas dimensões existentes.  
  
7.  Na página **Selecionar Chaves de Dimensão Ausentes** , selecione uma chave para a dimensão e, em seguida, clique em **Avançar**.  
  
    > [!NOTE]  
    >  A página **Selecionar Chaves de Dimensão Ausentes** será exibida se as tabelas de dimensão especificadas não tiverem uma chave definida.  
  
8.  Na página **Concluindo o Assistente** , digite um nome para o novo cubo e examine a estrutura do cubo. Se você quiser fazer mudanças, clique em **Voltar**; caso contrário, clique em **Concluir**.  
  
    > [!NOTE]  
    >  Você pode usar o Designer de Cubo para configurar o cubo após concluir o Assistente para Cubos. Você pode usar o Designer de Dimensão para adicionar, remover e configurar atributos e hierarquias nas dimensões criadas.  
  
  