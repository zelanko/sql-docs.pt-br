---
title: 'Etapa 2: Convertendo o projeto para o modelo de implantação de projeto | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba6dcb7052fed3d209dd87f55789a99df24116c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767348"
---
# <a name="step-2-converting-the-project-to-the-project-deployment-model"></a>Etapa 2: Convertendo o projeto para o modelo de implantação de projeto
  Nesta tarefa, você usará o Assistente de conversão de projeto do Integration Services para converter o projeto para o modelo de implantação do projeto.  
  
### <a name="converting-the-project-to-the-project-deployment-model"></a>Convertendo o projeto para o modelo de implantação de projeto  
  
1.  No Menu Projeto, clique em Converter em modelo de implantação de projeto.  
  
2.  Na página de Introdução do Assistente de conversão de projeto do Integration Services, revise as etapas e clique em Avançar.  
  
3.  Na página Selecionar pacotes, na lista Pacotes, desmarque todas as caixas de seleção exceto Lição 6.dtsx e então clique em Avançar.  
  
4.  Na página Especificar propriedades do projeto, clique em Avançar.  
  
5.  Na página Atualizar tarefa de execução do pacote, clique em Avançar.  
  
6.  Na página Selecionar configurações, verifique se que o pacote da Lição 6.dtsx está selecionado na lista Configurações e clique em Avançar.  
  
7.  Na página Criar parâmetros, verifique se o pacote Lição 6.dtsx está selecionado e se o Escopo está definido como Pacote na lista de Propriedades de configuração; em seguida, clique em Avançar.  
  
8.  Na página Configurar parâmetros, verifique se os valores de Nome e Valor são os mesmos nome e valor especificados na Lição 5 para a variável e o valor de configuração; então, clique em Avançar.  
  
9. Na página Revisar, no painel Resumo, observe que o assistente usou as informações do arquivo de configuração para definir as Propriedades a serem convertidas.  
  
10. Clique em Converter.  
  
     Quando a conversão for concluída, uma mensagem é exibida avisando que as alterações não serão salvas até que o projeto seja salvo no Visual Studio. Clique em OK na caixa de diálogo de aviso.  
  
11. No Assistente de conversão de projeto do Integration Services, clique em Fechar.  
  
12. No SQL Server Data Tools, clique no menu Arquivo e então em Salvar para salvar o pacote convertido.  
  
13. Clique na guia parâmetros e verifique se o pacote agora contém um parâmetro para VarFolderName e o valor é o mesmo caminho especificado para a pasta Novos dados de exemplo, do arquivo de configuração da Lição 5.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 3: Testando o pacote da lição 6](lesson-6-3-testing-the-lesson-6-package.md)  
  
  
