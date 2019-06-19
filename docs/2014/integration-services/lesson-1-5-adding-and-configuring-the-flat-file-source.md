---
title: 'Etapa 5: Adicionando e configurando o simples de fonte de arquivo | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32b95a5d156ae52394b7128b024c86b9a7e308b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891534"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>Etapa 5: Adicionar e configurar a fonte de arquivo simples
  Nesta tarefa, você irá adicionar e configurar uma fonte de arquivo simples ao seu pacote. Uma fonte de arquivo simples é um componente de fluxo de dados que usa metadados definidos por um gerenciador de conexões de arquivo simples para especificar o formato e a estrutura dos dados que serão extraídos do arquivo simples por um processo de transformação. Uma fonte de arquivo simples pode ser configurada para extrair dados de uma única fonte de arquivo simples usando a definição de formato de arquivo fornecida pelo gerenciador de conexões do arquivo simples.  
  
 Para este tutorial, você irá configurar a fonte de arquivo simples para usar o `Sample Flat File Source Data` Gerenciador de conexão que você criou anteriormente.  
  
### <a name="to-add-a-flat-file-source-component"></a>Para adicionar um componente Fonte de Arquivo Simples  
  
1.  Abra o **fluxo de dados** designer, clicando duas vezes o `Extract Sample Currency Data` tarefa de fluxo de dados ou clicando o **guia fluxo de dados**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Outras Fontes**e arraste uma **Fonte de Arquivo Simples** até a superfície de design da guia **Fluxo de Dados** .  
  
3.  Sobre o **fluxo de dados** superfície de design, clique com botão direito recém-adicionada **fonte de arquivo simples**, clique em **Renomear**e altere o nome para `Extract Sample Currency Data`.  
  
4.  Clique duas vezes na Fonte de Arquivo Simples para abrir a caixa de diálogo Editor da Fonte de Arquivo Simples.  
  
5.  No **Gerenciador de conexão de arquivo simples** caixa, selecione `Sample Flat File Source Data`.  
  
6.  Clique em **Colunas** e verifique se os nomes das colunas estão corretos.  
  
7.  Clique em **OK**.  
  
8.  Clique com o botão direito do mouse na fonte de Arquivo Simples e clique em **Propriedades**.  
  
9. Na janela Propriedades, verifique se o `LocaleID` estiver definida como **inglês (Estados Unidos)** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 6: Adicionando e configurando a transformação pesquisa](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fonte de Arquivo Simples](data-flow/flat-file-source.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)  
  
  
