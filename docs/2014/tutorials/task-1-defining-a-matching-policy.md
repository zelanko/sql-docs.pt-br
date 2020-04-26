---
title: 'Tarefa 1: definindo uma política de correspondência | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3e4777cf05e7f3eab62c389ace8b8d8a96cae304
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481311"
---
# <a name="task-1-defining-a-matching-policy"></a>Tarefa 1: Definindo uma política de correspondência
  Nesta tarefa, você criará uma política de correspondência com uma regra nela. A regra terá um pré-requisito: **ID do fornecedor**, o que significa que as IDs do fornecedor devem corresponder antes de usar os outros domínios na regra. A regra usa dois outros domínios: **nome do fornecedor** com o valor de **similaridade** definido como **70%** e **email de contato** com o valor de **similaridade** definido como **30%**.  
  
1.  Na página principal do **cliente do DQS**, clique na **seta para a direita** ao lado da base de dados de conhecimento **fornecedores** e selecione **política de correspondência**.  
  
     ![Menu Política de Correspondência na página principal](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "Menu Política de Correspondência na página principal")  
  
2.  Na página **mapa** , selecione **arquivo do Excel** para **fonte de dados**.  
  
3.  Clique em **procurar**, verifique se o filtro está definido como **pasta de trabalho do Excel**e selecione o arquivo **. xls da lista de fornecedores limpos** que você exportou depois de executar a atividade de limpeza.  
  
    > [!NOTE]  
    >  No final dessa atividade, você não poderá exportar os resultados, pois ela é centralizada basicamente na definição de uma política de correspondência. Você criará um Projeto de Qualidade de Dados para a atividade de correspondência e o executará para remover as duplicatas da lista de fornecedores usando essa política de correspondência na próxima lição.  
  
4.  Mapeie a coluna **CódigoDoFornecedor** para **domínio ID** do fornecedor, coluna **nome do fornecedor** para **nome do fornecedor** domínio, **ContactEmailAddress** coluna para contatar o domínio de **email** . Você só precisa mapear as colunas de origem para domínios que queira usar na definição da política de correspondência. Nesse caso, você está tornando os domínios Supplier ID, Supplier Name e Contact Email disponíveis para a atividade de política de correspondência.  
  
     ![Página Mapa do Processo de Definição da Política de Correspondência](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "Página Mapa do Processo de Definição da Política de Correspondência")  
  
5.  Clique em **Avançar** para ir para a página de **política de correspondência** , na qual você definirá uma política de correspondência com uma regra.  
  
6.  Clique no botão **criar uma regra de correspondência** na barra de ferramentas para criar uma regra na política.  
  
     ![Botão de barra de ferramentas Criar uma Regra Correspondente](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "Botão de barra de ferramentas Criar uma Regra Correspondente")  
  
7.  No painel **detalhes da regra** à direita, digite **remover fornecedores duplicados** para o **nome da regra**.  
  
8.  Clique em **Adicionar um novo elemento de domínio** na barra de ferramentas no painel direito.  
  
     ![Detalhes de regra - Botão Adicionar um Novo Elemento de Domínio](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "Detalhes de regra - Botão Adicionar um Novo Elemento de Domínio")  
  
9. Selecione **ID do fornecedor** para o **domínio** e marque a caixa de seleção de **pré-requisitos** . Observe que a **similaridade** é definida automaticamente como **exata**. Ao definir a **ID do fornecedor** como o **pré-requisito**, você especifica que os valores desse campo nos dois registros devem retornar uma correspondência de 100%, caso contrário, os registros não serão considerados uma correspondência e as outras cláusulas da regra serão desconsideradas.  
  
     ![Definição da regra Remover Fornecedores Duplicados](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "Definição da regra Remover Fornecedores Duplicados")  
  
10. Clique em **Adicionar um novo elemento de domínio** da barra de ferramentas novamente.  
  
11. Selecione **nome do fornecedor** domínio, selecione **semelhante** a **similaridade**e digite **70** para o **peso**.  Aqui, você está especificando que os nomes de fornecedor não precisam ser idênticos, mas podem ser semelhantes para que os registros sejam considerados uma correspondência. O peso indica a contribuição da pontuação desse campo para a pontuação de correspondência geral.  
  
12. Repita as duas etapas anteriores para adicionar o domínio de **email de contato** com **30** para o **peso**.  
  
13. Observe que a **Pontuação de correspondência mínima** está definida como **80%**, que é o valor que você vê na guia **geral** da página de **configuração** da **Administração do DQS**. Você só poderá aumentar essa pontuação acima desse valor de limite aqui.  
  
14. Observe que a opção **clusters sobrepostos** está selecionada. Com essa opção, um registro pode aparecer em vários clusters. Se você alterar a configuração para Clusters Não Sobrepostos, os clusters que tiverem registros comuns serão combinados em um único cluster.  
  
15. O botão **Iniciar** nessa página permite testar cada regra na política separadamente, enquanto que o botão Iniciar na próxima página permite que você teste toda a política (todas as regras na política).  
  
16. Clique em **Avançar** para alternar para a página **resultados de correspondência** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2: Testando e publicando a política de correspondência](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
