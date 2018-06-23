---
title: 'Tarefa 1: Definindo uma política de correspondência | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b0ccf6217899b5368cf27f93951e0a7ddc0cf48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013475"
---
# <a name="task-1-defining-a-matching-policy"></a>Tarefa 1: Definindo uma política de correspondência
  Nesta tarefa, você criará uma política de correspondência com uma regra nela. A regra terá um pré-requisito: **Supplier ID**, que significa que as IDs de fornecedor deverão corresponder antes de usar os outros domínios na regra. A regra usa dois outros domínios: **Supplier Name** com **similaridade** valor definido como **70%** e **Contact Email** com  **Similaridade** valor definido como **30%**.  
  
1.  Na página principal do **cliente DQS**, clique em **seta para a direita** lado **fornecedores** knowledge base e selecione **política de correspondência**.  
  
     ![Correspondência de Menu política principal página](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "correspondência política Menu principal página")  
  
2.  Sobre o **mapa** página, selecione **arquivo do Excel** para **fonte de dados**.  
  
3.  Clique em **procurar**, certifique-se de que o filtro é definido como **pasta de trabalho do Excel**e selecione **Cleansed Supplier List.xls** arquivo que você exportou depois de executar a atividade de limpeza.  
  
    > [!NOTE]  
    >  No final dessa atividade, você não poderá exportar os resultados, pois ela é centralizada basicamente na definição de uma política de correspondência. Você criará um Projeto de Qualidade de Dados para a atividade de correspondência e o executará para remover as duplicatas da lista de fornecedores usando essa política de correspondência na próxima lição.  
  
4.  Mapa **SupplierID** coluna **Supplier ID** domínio, **Supplier Name** coluna **Supplier Name** domínio  **ContactEmailAddress** coluna **Contact Email** domínio. Você só precisa mapear as colunas de origem para domínios que queira usar na definição da política de correspondência. Nesse caso, você está tornando os domínios Supplier ID, Supplier Name e Contact Email disponíveis para a atividade de política de correspondência.  
  
     ![Mapear a página do processo de definição de política de correspondência](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "mapear a página do processo de definição de política de correspondência")  
  
5.  Clique em **próximo** para mover para o **política de correspondência** página onde você definirá uma política de correspondência com uma regra nela.  
  
6.  Clique em **criar uma regra de correspondência** na barra de ferramentas para criar uma regra na política.  
  
     ![Criar um botão de barra de ferramentas de regra correspondente](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "criar um botão de barra de ferramentas de regra correspondente")  
  
7.  No **detalhes da regra** painel à direita, digite **remover fornecedores duplicados** para o **o nome da regra**.  
  
8.  Clique em **adicionar um novo elemento de domínio** na barra de ferramentas no painel direito.  
  
     ![Detalhes de regra - adicionar um novo botão de elemento de domínio](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "detalhes de regra - adicionar um novo botão de elemento de domínio")  
  
9. Selecione **Supplier ID** para o **domínio** e selecione o **pré-requisito** caixa de seleção. Observe que **similaridade** é definida automaticamente como **exato**. Definindo **Supplier ID** como o **pré-requisito**, você especificar que os valores para esse campo em dois registros diferentes devem retornar uma correspondência de 100%, ou os registros não serão considerados uma correspondência e as outras cláusulas no regra serão desconsideradas.  
  
     ![Remover definição de regra de fornecedores duplicados](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "remover fornecedores duplicados definição de regra")  
  
10. Clique em **adicionar um novo elemento de domínio** na barra de ferramentas novamente.  
  
11. Selecione **Supplier Name** domínio, selecione **Similar** para **similaridade**e o tipo **70** para o **peso**.  Aqui, você está especificando que os nomes de fornecedor não precisam ser idênticos, mas podem ser semelhantes para que os registros sejam considerados uma correspondência. O peso indica a contribuição da pontuação desse campo para a pontuação de correspondência geral.  
  
12. Repita as duas etapas anteriores para adicionar **Contact Email** domínio com **30** para o **peso**.  
  
13. Observe que o **min pontuação de correspondência** é definido como **80%**, que é o valor que você vê no **geral** guia do **configuração** página do **Administração do DQS**. Você só poderá aumentar essa pontuação acima desse valor de limite aqui.  
  
14. Observe que **Clusters sobrepostos** opção é selecionada. Com essa opção, um registro pode aparecer em vários clusters. Se você alterar a configuração para Clusters Não Sobrepostos, os clusters que tiverem registros comuns serão combinados em um único cluster.  
  
15. O **iniciar** botão nesta página permite testar cada regra na política separadamente, enquanto o botão Iniciar na próxima página permite que você teste a política inteira (todas as regras na política).  
  
16. Clique em **próximo** para alternar para o **resultados de correspondência** página.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2: Testando e publicando a política de correspondência](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  