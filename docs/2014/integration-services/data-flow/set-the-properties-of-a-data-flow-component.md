---
title: Definir as propriedades de um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc360da93b905bed20f118812898b5c029c570cf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770725"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>Definir as propriedades de um componente de fluxo de dados
  Para definir as propriedades de componentes de fluxo de dados, que incluem origens, destinos e transformações, use um dos seguintes recursos:  
  
-   Os editores de componente fornecidos pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses editores incluem somente as propriedades personalizadas de cada componente de fluxo de dados.  
  
-   A janela **Propriedades** lista as propriedades personalizadas no nível do componente de cada elemento, bem como as propriedades comuns a todos os elementos do fluxo de dados.  
  
-   A caixa de diálogo **Editor Avançado** fornece acesso a propriedades personalizadas para cada componente. A caixa de diálogo **Editor Avançado** também fornece acesso a propriedades comuns a todos os componentes de fluxo de dados: as propriedades de entradas, saídas, saídas de erro, colunas e colunas externas.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>Para definir as propriedades de um componente de fluxo de dados usando um editor de componente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados com os componentes cujas propriedades você deseja exibir e modificar.  
  
4.  Clique duas vezes no componente de fluxo de dados.  
  
5.  No editor de componente, exiba ou modifique os valores de propriedade e feche o editor.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>Para definir as propriedades de um componente de fluxo de dados usando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém os componentes cujas propriedades você deseja exibir e modificar.  
  
4.  Clique com o botão direito do mouse no componente do fluxo de dados e clique em **Propriedades**.  
  
5.  Exiba ou modifique os valores de propriedade e então feche a janela **Propriedades** .  
  
    > [!NOTE]  
    >  Muitas propriedades são somente leitura e não podem ser modificadas.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>Para definir as propriedades de um componente de fluxo de dados usando o Editor Avançado  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o componente que deseja exibir ou modificar.  
  
4.  No designer de fluxo de dados, clique com o botão direito do mouse no componente de fluxo de dados e clique em **Mostrar Editor Avançado**.  
  
    > [!NOTE]  
    >  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os componentes de fluxo de dados que dão suporte a diversas entradas não podem usar o **Editor Avançado**.  
  
5.  Na caixa de diálogo **Editor Avançado** , execute uma das seguintes etapas:  
  
    -   Para exibir e especificar a conexão usada pelo componente, clique na guia **Gerenciadores de Conexões** .  
  
        > [!NOTE]  
        >  A guia **Gerenciadores de Conexões** está disponível apenas para componentes de fluxo de dados que usam gerenciadores de conexões para se conectar com fontes de dados como arquivos e bancos de dados  
  
    -   Para exibir e modificar propriedades no nível do componente, clique na guia **Propriedades do Componente** .  
  
    -   Para exibir ou modificar mapeamentos entre colunas externas e a saída disponível, clique na guia **Mapeamentos de Coluna** .  
  
        > [!NOTE]  
        >  A guia **Mapeamentos de Coluna** está disponível apenas ao exibir ou editar origens ou destinos.  
  
    -   Para exibir uma lista das colunas de entrada disponíveis e atualizar os nomes das colunas de saída, clique na guia **Colunas de Entrada** .  
  
        > [!NOTE]  
        >  A guia Colunas de Entrada só fica disponível ao trabalhar com transformações ou destinos. Para obter mais informações, consulte [Integration Services Transformations](transformations/integration-services-transformations.md).  
  
    -   Para exibir e modificar as propriedades de entradas, saídas e saídas de erro e as propriedades das colunas que elas contêm, clique na guia **Propriedades de Entrada e Saída** .  
  
        > [!NOTE]  
        >  Origens não têm entradas. Destinos não têm saídas, exceto uma saída de erro opcional.  
  
6.  Exiba ou modifique os valores de propriedade.  
  
7.  Clique em **OK**.  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="see-also"></a>Consulte Também  
 [Transformações do Integration Services](transformations/integration-services-transformations.md)  
  
  
