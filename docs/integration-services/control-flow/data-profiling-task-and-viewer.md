---
title: Visualizador e tarefa criação de perfil de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2aab2b6a4c19ed5cb8d3e1d5ea73af57cb6e506e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831654"
---
# <a name="data-profiling-task-and-viewer"></a>Tarefa e visualizador da tarefa Criação de Perfil de Dados
  A tarefa Criação de Perfil de Dados fornece a funcionalidade de criação de perfil de dados dentro do processo de extração, transformação e carga de dados. Usando a tarefa Criação de Perfil de Dados, você pode alcançar os seguintes benefícios:  
  
-   Analisar os dados de origem mais efetivamente  
  
-   Entender melhor os dados de origem  
  
-   Prevenir problemas de qualidade dos dados antes que eles sejam introduzidos no data warehouse.  
  
> [!IMPORTANT]  
>  A tarefa Criação de Perfil de Dados funciona apenas com dados armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ela não funciona com fontes de dados de terceiros ou baseadas em arquivos.  
  
## <a name="data-profiling-overview"></a>Visão geral da Criação de Perfil de Dados  
 A qualidade dos dados é importante para todo negócio. Como as empresas constroem sistemas analíticos e de business intelligence no topo de seus sistemas transacionais, a confiabilidade dos indicadores chave de desempenho e das previsões da mineração de dados, depende completamente da validade dos dados onde eles são baseados. Mas, embora a importância da validade dos dados para a realização das decisões de negócios esteja crescendo, o desafio de certificar-se da validade dos dados também está aumentando. Dentro da empresa os dados estão fluindo constantemente de diversos sistemas e fontes e de um grande número de usuários.  
  
 Métrica para qualidade de dados pode ser difícil de definir porque eles são específicos ao domínio ou aplicativo. Uma abordagem comum para definir qualidade de dados é a criação de perfil de dados.  
  
 Um perfil de dados é uma coleção de estatísticas de agregação sobre os dados que podem incluir o seguinte:  
  
-   O número de linhas na tabela Cliente.  
  
-   O número de valores distintos na coluna Estado.  
  
-   O número de valores ausentes ou nulos na coluna Zip.  
  
-   A distribuição de valores na coluna Cidade.  
  
-   A intensidade da dependência funcional da coluna Estado na coluna Zip, ou seja, o Estado deve sempre ser o mesmo para determinado valor de Zip.  
  
 As estatísticas que a criação de perfil de dados provê, fornecem a informação necessária para efetivamente minimizar as perdas de qualidade que podem ocorrer do uso da fonte de dados.  
  
## <a name="integration-services-and-data-profiling"></a>Integration Services e criação de perfil de dados  
 Em [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o processo de criação de perfil de dados consiste nas seguintes etapas:  
  
 **Etapa 1: Definindo a tarefa Criação de Perfil de Dados**  
 A tarefa Criação de Perfil de Dados é uma tarefa que você usa para configurar os perfis que deseja calcular. Você executa o pacote que contém a tarefa de Criação de Perfil de Dados para computar os perfis. A tarefa salva o perfil produzido em formato de XML em um arquivo ou uma variável de pacote.  
  
 **Para obter mais informações:** [Instalação da Tarefa de Criação de Perfil de Dados](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)  
  
 **Etapa 2: Revisando os perfis que a tarefa Criação de Perfis de Dados computa**  
 Para exibir os perfis de dados que a tarefa Criação de Perfil de Dados computa, envie a saída para um arquivo e utilize o Visualizador de Perfil de dados Esse visualizador é um utilitário autônomo que mostra a saída do perfil em formato resumido e detalhado com uma capacidade opcional de busca.  
  
 **Para obter mais informações:** [Visualizador de Perfil de Dados](../../integration-services/control-flow/data-profile-viewer.md)  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>Adição de lógica condicional ao fluxo de trabalho de criação de perfil de dados.  
 A tarefa Criação de Perfil de Dados não tem recursos internos que lhe permitam usar lógica condicional para conectar essa tarefa a tarefas de downstream com base na saída do perfil. Porém, você pode adicionar facilmente esta lógica, com uma quantidade pequena de programação, em uma tarefa de Script. Por exemplo, a tarefa Script poderia executar uma consulta XPath contra o arquivo de saída da tarefa de Criação de Perfil de Dados. A consulta poderia determinar se a porcentagem de valores nulos em uma coluna particular excede certo limite. Se a porcentagem exceder o limite, você pode interromper o pacote e resolver o problema na fonte de dados antes de continuar. Para obter informações, consulte [Incorporar uma tarefa Criação de Perfil de Dados no fluxo de trabalho do pacote](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Esquema do criador de perfil de dados](http://go.microsoft.com/fwlink/?LinkId=251524)  
  
  
