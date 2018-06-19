---
title: 'Etapa 5: Adicionando e configurando a fonte de arquivo simples | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4d1b0767564d0e664d14af285617f8ae0947382d
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35329310"
---
# <a name="lesson-1-5---adding-and-configuring-the-flat-file-source"></a>Lição 1-5 – adicionar e configurar a fonte de arquivo simples
Nesta tarefa, você irá adicionar e configurar uma fonte de arquivo simples ao seu pacote. Uma fonte de arquivo simples é um componente de fluxo de dados que usa metadados definidos por um gerenciador de conexões de arquivo simples para especificar o formato e a estrutura dos dados que serão extraídos do arquivo simples por um processo de transformação. Uma fonte de arquivo simples pode ser configurada para extrair dados de uma única fonte de arquivo simples usando a definição de formato de arquivo fornecida pelo gerenciador de conexões do arquivo simples.  
  
Para este tutorial, você irá configurar a fonte de arquivo simples para usar o gerenciador de conexões **Dados da Fonte de Arquivo Simples de Exemplo** criada anteriormente.  
  
### <a name="to-add-a-flat-file-source-component"></a>Para adicionar um componente Fonte de Arquivo Simples  
  
1.  Abra o designer **Fluxo de Dados** clicando duas vezes na tarefa de fluxo de dados **Extrair Dados de Moeda de Exemplo** ou clicando na **guia Fluxo de Dados**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Outras Fontes**e arraste uma **Fonte de Arquivo Simples** até a superfície de design da guia **Fluxo de Dados** .  
  
3.  Na superfície de design **Fluxo de Dados** , clique com o botão direito do mouse na **Fonte de Arquivo Simples**recém-adicionada, clique em **Renomear**e altere o nome para **Extrair Dados de Moeda de Exemplo**.  
  
4.  Clique duas vezes na Fonte de Arquivo Simples para abrir a caixa de diálogo Editor da Fonte de Arquivo Simples.  
  
5.  Na caixa **Gerenciador de conexões de arquivo simples** , selecione **Dados de Exemplo da Fonte de Arquivo Simples**.  
  
6.  Clique em **Colunas** e verifique se os nomes das colunas estão corretos.  
  
7.  Clique em **OK**.  
  
8.  Clique com o botão direito do mouse na fonte de Arquivo Simples e clique em **Propriedades**.  
  
9. Na janela Propriedades, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 6: Adicionando e configurando a transformação Pesquisa](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Consulte Também  
[Fonte de Arquivo Simples](../integration-services/data-flow/flat-file-source.md)  
[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
  
  
