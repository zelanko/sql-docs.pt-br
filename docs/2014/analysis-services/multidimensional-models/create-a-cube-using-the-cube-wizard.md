---
title: Criar um cubo usando o assistente para cubos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], creating
ms.assetid: d46d659c-3a4e-4364-94ac-f5eb6ba0ec25
author: minewiskan
ms.author: owend
ms.openlocfilehash: 79a675d0d27c5bfe033075c92e7ed06aa9c914c5
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536704"
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
  
    3.  Clique em **Próximo**.  
  
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
  
  
