---
title: 'Etapa 2: converter o projeto para o modelo de implantação de projeto | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f7097d75078c8602172e2e16a26832ab4bb385a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-6-2---converting-the-project-to-the-project-deployment-model"></a>Lição 6-2 – converter o projeto para o modelo de implantação de projeto
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
[Etapa 3: Testando o pacote da Lição 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
