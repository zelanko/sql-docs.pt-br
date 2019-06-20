---
title: 'Tarefa 1: Definindo uma política de correspondência | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481311"
---
# <a name="task-1-defining-a-matching-policy"></a>Tarefa 1: Definir uma política de correspondência
  Nesta tarefa, você criará uma política de correspondência com uma regra nela. A regra terá um pré-requisito: **Supplier ID**, que significa que as IDs de fornecedor deverão corresponder antes do uso de outros domínios na regra. A regra usa dois outros domínios: **Nome do fornecedor** com **similaridade** valor definido como **70%** e **Contact Email** com **similaridade** valor definido como **30%** .  
  
1.  Na página principal do **cliente DQS**, clique em **seta para a direita** lado **fornecedores** knowledge base e selecione **política de correspondência**.  
  
     ![Menu de política no principal de correspondência página](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "correspondência de Menu de política na principal página")  
  
2.  Sobre o **mapa** página, selecione **arquivo do Excel** para **fonte de dados**.  
  
3.  Clique em **navegue**, certifique-se de que o filtro é definido como **pasta de trabalho do Excel**e selecione **Cleansed Supplier List** que você exportou depois de executar a atividade de limpeza de arquivo.  
  
    > [!NOTE]  
    >  No final dessa atividade, você não poderá exportar os resultados, pois ela é centralizada basicamente na definição de uma política de correspondência. Você criará um Projeto de Qualidade de Dados para a atividade de correspondência e o executará para remover as duplicatas da lista de fornecedores usando essa política de correspondência na próxima lição.  
  
4.  Mapa **SupplierID** coluna a ser **Supplier ID** domínio **Supplier Name** coluna a ser **Supplier Name** domínio,  **ContactEmailAddress** coluna para **Contact Email** domínio. Você só precisa mapear as colunas de origem para domínios que queira usar na definição da política de correspondência. Nesse caso, você está tornando os domínios Supplier ID, Supplier Name e Contact Email disponíveis para a atividade de política de correspondência.  
  
     ![Mapear a página do processo de definição de política de correspondência](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "mapear a página do processo de definição de política de correspondência")  
  
5.  Clique em **próxima** para mover para o **política de correspondência** página onde você definirá uma política de correspondência com uma regra nela.  
  
6.  Clique em **criar uma regra de correspondência** na barra de ferramentas para criar uma regra na política.  
  
     ![Criar um botão de barra de ferramentas de regra correspondente](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "criar um botão de barra de ferramentas de regra correspondente")  
  
7.  No **detalhes da regra** painel à direita, insira **remover fornecedores duplicados** para o **nome da regra**.  
  
8.  Clique em **adicionar um novo elemento de domínio** na barra de ferramentas no painel direito.  
  
     ![Detalhes de regra - adicionar um novo botão de elemento de domínio](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "detalhes de regra - adicionar um novo botão de elemento de domínio")  
  
9. Selecione **Supplier ID** para o **domínio** e selecione o **pré-requisito** caixa de seleção. Observe que **similaridade** é automaticamente definido como **Exact**. Definindo **Supplier ID** como o **pré-requisito**, você especificar que os valores para esse campo em dois registros diferentes devem retornar uma correspondência de 100%, ou os registros não serão considerados uma correspondência e as outras cláusulas no regra serão desconsideradas.  
  
     ![Remover definição de regra de fornecedores duplicados](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "remover fornecedores duplicados definição de regra")  
  
10. Clique em **adicionar um novo elemento de domínio** na barra de ferramentas novamente.  
  
11. Selecione **Supplier Name** domínio, selecione **Similar** para **similaridade**e o tipo **70** para o **peso**.  Aqui, você está especificando que os nomes de fornecedor não precisam ser idênticos, mas podem ser semelhantes para que os registros sejam considerados uma correspondência. O peso indica a contribuição da pontuação desse campo para a pontuação de correspondência geral.  
  
12. Repita as duas etapas anteriores para adicionar **Contact Email** domínio com **30** para o **peso**.  
  
13. Observe que o **min pontuação de correspondência** é definido como **80%** , que é o valor que você vê no **geral** guia do **configuração** página do **Administração do DQS**. Você só poderá aumentar essa pontuação acima desse valor de limite aqui.  
  
14. Observe que **Clusters sobrepostos** opção está selecionada. Com essa opção, um registro pode aparecer em vários clusters. Se você alterar a configuração para Clusters Não Sobrepostos, os clusters que tiverem registros comuns serão combinados em um único cluster.  
  
15. O **iniciar** botão nesta página lhe permite testar cada regra na política separadamente, por outro lado, o botão Iniciar na próxima página permite que você teste a política inteira (todas as regras na política).  
  
16. Clique em **próxima** para alternar para o **resultados de correspondência** página.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2: Testando e publicando a política de correspondência](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
