---
title: Mapear conjuntos de resultados para variáveis em uma tarefa Executar SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 995afe55c1cd1b7d925c9267ba5dfa3aed038358
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057754"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>Mapear conjuntos de resultados para variáveis em uma tarefa Executar SQL
  Este tópico descreve como criar um mapeamento entre um conjunto de resultados e uma variável em uma tarefa Executar SQL. O mapeamento de um conjunto de resultados para uma variável disponibiliza o conjunto de resultados para outros elementos no pacote. Por exemplo, um script em uma tarefa Script pode ler a variável e usar os valores do conjunto de resultados; ou uma origem XML pode consumir o conjunto de resultados armazenado em uma variável. Se o conjunto de resultados for gerado por um pacote pai, ele poderá ser disponibilizado para um pacote filho chamado por uma tarefa Executar Pacote, mapeando o conjunto de resultados para uma variável no pacote pai e, em seguida, criando uma configuração de variável de pacote pai no pacote filho para armazenar o valor da variável pai.  
  
 Para obter descrições dos diferentes tipos de conjuntos de resultados e tipos de dados variáveis que podem ser mapeados para os conjuntos de resultados, consulte [Conjuntos de resultados na tarefa Executar SQL](control-flow/execute-sql-task.md).  
  
### <a name="to-map-a-result-set-to-a-variable"></a>Para mapear um conjunto de resultados para uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No **Gerenciador de Soluções**, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Se o pacote ainda não incluir uma tarefa Executar SQL, adicione uma ao fluxo de controle do pacote. Para obter mais informações, consulte [adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
5.  Clique duas vezes na tarefa Executar SQL.  
  
6.  Na caixa de diálogo **Editor da Tarefa Executar SQL** , na página **Geral** , selecione o tipo do conjunto de resultados, **Linha simples**, **Conjunto de resultados completo**ou **XML** .  
  
     Para obter descrições dos conjuntos de resultados diferentes, consulte [Conjuntos de resultados na tarefa Executar SQL](result-sets-in-the-execute-sql-task.md)  
  
7.  Clique em **Conjunto de Resultados**.  
  
8.  Para adicionar um mapeamento de conjunto de resultados, clique em **Adicionar**.  
  
9. Na lista **Nome de Variáveis** , selecione uma variável ou crie uma nova. Para obter mais informações, consulte [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
     Para obter descrições dos tipos de dados variáveis que podem ser mapeados para os diferentes conjuntos de resultados, consulte [Conjuntos de resultados na tarefa Executar SQL](result-sets-in-the-execute-sql-task.md).  
  
     Para obter informações sobre como mapear uma variável para uma única coluna e mapear diversas variáveis para várias colunas, consulte a seção **Populando uma variável com um conjunto de resultados** em [Conjuntos de resultados na tarefa Executar SQL](control-flow/execute-sql-task.md).  
  
10. Na lista **Nome do Resultado** , opcionalmente, modifique o nome do conjunto de resultados.  
  
     Em geral, você pode usar o nome da coluna como o nome do conjunto de resultados ou você pode usar a posição ordinal da coluna na lista de colunas como o conjunto de resultados. A capacidade de usar um nome de coluna como o nome do conjunto de resultados depende do provedor que a tarefa está configurada para usar. Nem todos os provedores tornam os nomes das colunas disponíveis.  
  
11. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Executar SQL](control-flow/execute-sql-task.md)   
 [Conjuntos de resultados na tarefa Executar SQL](result-sets-in-the-execute-sql-task.md)   
 [Tarefa executar pacote](control-flow/execute-package-task.md)   
 [Configurações do Pacote](../../2014/integration-services/package-configurations.md)   
 [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md)   
 [Use os valores de variáveis e parâmetros em um pacote filho](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md)  
  
  
