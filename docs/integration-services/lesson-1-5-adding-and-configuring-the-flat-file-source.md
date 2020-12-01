---
description: 'Lição 1-5: Adicionar e configurar a fonte de Arquivo Simples'
title: 'Etapa 5: Adicionar e configurar a fonte de Arquivo Simples | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cfc6ffa21bf3f6c1205b1c9c667cc6e75868cece
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88390862"
---
# <a name="lesson-1-5-add-and-configure-the-flat-file-source"></a>Lição 1-5: Adicionar e configurar a fonte de Arquivo Simples

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Nesta tarefa, você adiciona e configura uma fonte de arquivo simples ao seu pacote. Uma fonte de arquivo simples é um componente de fluxo de dados que usa metadados definidos por um gerenciador de conexões de Arquivo Simples. Esses metadados especificam o formato e a estrutura dos dados a serem extraídos do arquivo simples por um processo de transformação. A fonte de Arquivo Simples extrai dados de um único arquivo simples, usando as definições de formato no gerenciador de conexões de Arquivo Simples.  
  
Para esta tarefa, configure a fonte de arquivo simples para usar o gerenciador de conexões **Dados de Origem de Arquivo Simples de Exemplo** criada anteriormente.  
  
## <a name="add-a-flat-file-source-component"></a>Adicionar um componente de fonte de Arquivo Simples  
  
1.  Para abrir o designer de **Fluxo de Dados**, seja clicando duas vezes na tarefa de fluxo de dados **Extrair Dados de Moeda de Exemplo** ou clicando na guia **Fluxo de Dados**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Outras Fontes** e arraste uma **Fonte de Arquivo Simples** até a superfície de design da guia **Fluxo de Dados** .  
  
3.  Na superfície de design **Fluxo de Dados**, clique com o botão direito do mouse na **Fonte de Arquivo Simples** recém-adicionada, selecione **Renomear** e altere o nome para **Extrair Dados de Moeda de Exemplo**.  
  
4.  Clique duas vezes na Fonte de Arquivo Simples para abrir a caixa de diálogo **Editor da Fonte de Arquivo Simples**.  
  
5.  No campo **Gerenciador de conexões de arquivo simples**, selecione **Dados de Origem de Arquivo Simples de Exemplo**.  
  
6.  Selecione **Colunas** e verifique se os nomes das colunas estão corretos.  
  
7.  Selecione **OK**.  
  
8.  Clique com o botão direito do mouse na fonte de Arquivo Simples e selecione **Propriedades**.  
  
9. Na janela **Propriedades**, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)** .  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 6: Adicionar e configurar as transformações de Pesquisa](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Confira também  
[Origem de Arquivo Simples](../integration-services/data-flow/flat-file-source.md)  
[Gerenciador de Conexões de Arquivos Simples](../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
  
