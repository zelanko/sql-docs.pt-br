---
title: 'Etapa 5: Adicionando e configurando a fonte de arquivo simples | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f1f50c3aed4429a3ba05a23a969d050c45778c34
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435843"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>Etapa 5: Adicionar e configurar a fonte de arquivo simples
  Nesta tarefa, você irá adicionar e configurar uma fonte de arquivo simples ao seu pacote. Uma fonte de arquivo simples é um componente de fluxo de dados que usa metadados definidos por um gerenciador de conexões de arquivo simples para especificar o formato e a estrutura dos dados que serão extraídos do arquivo simples por um processo de transformação. Uma fonte de arquivo simples pode ser configurada para extrair dados de uma única fonte de arquivo simples usando a definição de formato de arquivo fornecida pelo gerenciador de conexões do arquivo simples.  
  
 Para este tutorial, você configurará a fonte de arquivo simples para usar o `Sample Flat File Source Data` Gerenciador de conexões que você criou anteriormente.  
  
### <a name="to-add-a-flat-file-source-component"></a>Para adicionar um componente Fonte de Arquivo Simples  
  
1.  Abra o designer de **fluxo de dados** clicando duas vezes na tarefa fluxo de dados `Extract Sample Currency Data` ou clicando na **guia fluxo de dados**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Outras Fontes**e arraste uma **Fonte de Arquivo Simples** até a superfície de design da guia **Fluxo de Dados** .  
  
3.  Na superfície de design do **fluxo de dados** , clique com o botão direito do mouse na **fonte de arquivo simples**recém-adicionada, clique em **renomear**e altere o nome para `Extract Sample Currency Data` .  
  
4.  Clique duas vezes na Fonte de Arquivo Simples para abrir a caixa de diálogo Editor da Fonte de Arquivo Simples.  
  
5.  Na caixa **Gerenciador de conexões de arquivo simples** , selecione `Sample Flat File Source Data` .  
  
6.  Clique em **Colunas** e verifique se os nomes das colunas estão corretos.  
  
7.  Clique em **OK**.  
  
8.  Clique com o botão direito do mouse na fonte de Arquivo Simples e clique em **Propriedades**.  
  
9. No janela Propriedades, verifique se a `LocaleID` propriedade está definida como **inglês (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 6: Adicionar e configurar a transformação Pesquisa](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Fonte de arquivo simples](data-flow/flat-file-source.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)  
  
  
