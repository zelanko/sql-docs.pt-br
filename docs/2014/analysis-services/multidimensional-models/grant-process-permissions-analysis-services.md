---
title: Conceder permissões de processo (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], process
- process permissions [Analysis Services]
ms.assetid: c1531c23-6b46-46a8-9ba3-b6d3f2016443
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 175e07432d3f67374710d6e33f3006f2b3b6bf68
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181251"
---
# <a name="grant-process-permissions-analysis-services"></a>Conceder permissões de processo (Analysis Services)
  Como administrador, você pode criar uma função dedicada às operações de processamento do Analysis Services, o que lhe permitirá delegar essa tarefa específica a outros usuários ou a aplicativos usados para o processamento autônomo agendado. As permissões de processo podem ser concedidas nos níveis de banco de dados, cubo, dimensão e estrutura de mineração. A menos que você esteja trabalhando com um grande cubo ou banco de dados de tabelas, recomendamos a concessão de direitos de processamento no nível de banco de dados, incluindo aqueles que apresentem dependências entre si.  
  
 As permissões são concedidas por meio de funções que associam objetos com permissões e contas de usuário ou de grupo do Windows. Lembre-se de que as permissões são aditivas. Se uma função concede permissão para processar um cubo, enquanto uma segunda função dá permissão ao mesmo usuário para processar uma dimensão, as permissões das duas diferentes funções se combinam para dar ao usuário permissão para processar o cubo e processar a dimensão especificada nesse banco de dados.  
  
> [!IMPORTANT]  
>  Um usuário cuja função tenha somente permissões para Processar não poderá usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para se conectar ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e processar os objetos. Essas ferramentas exigem o `Read Definition` permissão para acessar metadados do objeto. Sem a capacidade de usar nenhuma ferramenta, use um script XMLA para executar uma operação de processamento.  
>   
>  Sugerimos que você também conceda `Read Definition` permissões para fins de teste. Um usuário que tem `Read Definition` e `Process Database` permissões podem processar objetos em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]de forma interativa. Consulte [Grant read definition permissions on object metadata &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md) para ver mais detalhes.  
  
## <a name="set-processing-permissions-at-the-database-level"></a>Definir permissões de processamento no nível de banco de dados  
 Esta seção explica como habilitar o processamento de todos os cubos, dimensões, estruturas de mineração e modelos de mineração no banco de dados por não administradores.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra a pasta Bancos de Dados e selecione um banco de dados.  
  
2.  Clique com o botão direito do mouse em **Funções** | **Nova Função**. Insira um nome e uma descrição.  
  
3.  No **gerais** painel, selecione o `Process Database` caixa de seleção. Além disso, selecione `Read Definition` para permitir o processamento interativo por meio de uma das ferramentas do SQL Server, como também [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
4.  No painel **Associação** , adicione as contas de usuário e de grupo do Windows com permissão para processar qualquer objeto nesse banco de dados.  
  
5.  Clique em **OK** para concluir a definição de função.  
  
## <a name="set-processing-permissions-on-individual-objects"></a>Defina as permissões de processamento em objetos individuais  
 Você pode definir permissões de processamento em cubos individuais, dimensões, estruturas ou modelos de mineração de dados.  
  
 O processamento pode falhar se você acidentalmente excluir objetos que precisam ser processados em conjunto (por exemplo, se você habilitar o processamento em um cubo, mas não em suas dimensões relacionadas). Como pode ser fácil perder dependências de objeto, o teste completo é essencial ao definir as permissões de processamento em objetos individuais.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra a pasta Bancos de Dados e selecione um banco de dados.  
  
2.  Clique com o botão direito do mouse em **Funções** | **Nova Função**. Insira um nome e uma descrição.  
  
3.  No **gerais** painel, desmarque o `Process Database` caixa de seleção. As permissões de banco de dados substituem a capacidade de definir permissões em objetos de nível mais baixo, tornando as opções de função acinzentadas ou não selecionáveis.  
  
     Tecnicamente, nenhuma permissão de banco de dados é necessária para as funções de processamento dedicadas. Mas sem `Read Definition` no nível do banco de dados, não é possível exibir o banco de dados [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o que dificulta o teste.  
  
4.  Selecione objetos individuais para processar:  
  
    -   No painel **Cubos** , marque a caixa de seleção **Processar** para cada cubo.  
  
    -   No painel **Dimensões** , selecione **Todas as dimensões do banco de dados**e marque a caixa de seleção **Processar** para cada dimensão. Ou, selecione todas as linhas e use Shift + clique para alternar a caixa de seleção.  
  
5.  No painel **Associação** , adicione as contas de usuário e de grupo do Windows com permissão para processar esses objetos.  
  
6.  Clique em **OK** para concluir a definição de função.  
  
## <a name="test-processing"></a>Testar processamento  
  
1.  Mantenha pressionada a tecla Shift e clique com o botão direito do mouse em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione **Executar como um usuário diferente** e conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando uma conta do Windows atribuída à função a qual você está testando.  
  
2.  Abra a pasta Bancos de Dados e selecione um banco de dados. Você verá somente os bancos de dados visíveis às funções às quais a sua conta tenha associação.  
  
3.  Clique com o botão direito do mouse no cubo ou dimensão e selecione **Processar**. Escolha uma opção de processamento. Teste todas as opções para todas as combinações de objetos. Se ocorrerem erros devido a objetos ausentes, adicione os objetos à função.  
  
## <a name="set-processing-permissions-on-a-data-mining-structure"></a>Defina permissões de processamento em uma estrutura de mineração de dados  
 Você pode criar uma função que conceda permissão para processar estruturas de mineração de dados. Isso inclui o processamento de todos os modelos de mineração.  
  
 **Detalhar** e `Read Definition` permissões usadas para um modelo de mineração e uma estrutura de navegação são atômicas e podem ser adicionados à mesma função ou separados em uma função diferente.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra a pasta Bancos de Dados e selecione um banco de dados.  
  
2.  Clique com o botão direito do mouse em **Funções** | **Nova Função**. Insira um nome e uma descrição. No painel **Geral** , verifique se as caixas de seleção de permissão do banco de dados estão desmarcadas. As permissões de banco de dados substituirão a capacidade de definir permissões em objetos de nível mais baixo, tornando as opções de função acinzentadas ou não selecionáveis.  
  
3.  No painel **Estruturas de Mineração** , marque a caixa de seleção **Processar** para cada estrutura de mineração.  
  
4.  No painel **Associação** , adicione as contas de usuário e de grupo do Windows com permissão para processar qualquer objeto nesse banco de dados.  
  
5.  Clique em **OK** para concluir a definição de função.  
  
## <a name="see-also"></a>Consulte também  
 [Processar banco de dados, tabela ou partição](../tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Processamento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)   
 [Conceder permissões de banco de dados &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)   
 [Conceder permissões para ler definição em metadados de objetos &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
  
