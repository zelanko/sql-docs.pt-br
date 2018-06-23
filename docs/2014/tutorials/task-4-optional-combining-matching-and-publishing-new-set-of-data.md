---
title: 'Tarefa 4 (opcional): combinando, correspondendo e publicando o novo conjunto de dados | Microsoft Docs'
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
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4ab096c1f43fbeab2165e1e32a83f2ba854b3b13
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012602"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Tarefa 4 (Opcional): Combinando, correspondendo e publicando o novo conjunto de dados
  Com o tempo, você desejará adicionar mais dados ao repositório do MDS. Antes de adicionar dados, ele pode ser útil comparar os novos dados aos dados que já são gerenciados no MDS, para garantir que você não está adicionando dados duplicados ou inexatos. No Suplemento Master Data Services para Excel, você pode combinar dados de duas planilhas e comparar esses dados para identificar e remover duplicatas antes de publicar os dados no MDS. O recurso de correspondência do Suplemento MDS do Excel usa a funcionalidade correspondente do DQS para identificar correspondências nos dados. Nesta tarefa, você combinará dados de duas planilhas em uma e executará a atividade de correspondência para identificar e remover duplicatas antes de publicar no MDS. Consulte [correspondência de qualidade de dados em que o suplemento do MDS para Excel](http://msdn.microsoft.com/library/hh548681.aspx) e [combinar dados](http://msdn.microsoft.com/library/hh548680.aspx) tópicos para obter mais detalhes.  
  
1.  Iniciar nova instância da **Excel**. Clique em **iniciar**, aponte para **executar**, tipo **Excel**e clique em **Okey**.  
  
2.  Alterne para o **dados mestres** guia clicando **dados mestres** na barra de menus.  
  
3.  Clique em **conectar** na faixa de opções no **conectar e carregar** grupo para se conectar ao **servidor MDS**. Você configurou essa conexão anteriormente nesta lição.  
  
     ![Excel - Mostrar botão Gerenciador em dados mestre](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - Mostrar botão Gerenciador em dados mestre")  
  
4.  Você deve ver o **Master Data Explorer** painel à direita. Se você não vir o Master Data Explorer, clique em **Mostrar Explorer** botão na faixa de opções.  
  
5.  No **Master Data Explorer** janela, selecione **fornecedores** na lista suspensa para o **modelo**. Você verá que o modelo tem uma entidade: **Supplier**.  
  
     ![Excel - janela Master Data Explorer](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - janela Master Data Explorer")  
  
6.  Clique duas vezes em **fornecedor** na lista de entidades para carregar os membros da entidade na planilha do Excel.  
  
7.  Clique em **Planilha2** na parte inferior para alternar para o **Planilha2** guia. Se você não vir **Planilha2**, adicione uma nova planilha.  
  
8.  Abra **Suppliers.xls** arquivo (o arquivo de entrada original que está incluído nos arquivos de tutorial) e copie todas as linhas (três) do **CombineAndCleanse** planilha para **Planilha2**.  
  
9. Volte para o **Supplier** planilha no **livro 1 – Microsoft Excel** (não o **Cleansed and Matched Supplier List** Excel) que está conectado à **MDS**.  
  
10. Clique em **Dados Mestres** na barra de menus.  
  
11. Clique em **combinar dados** na faixa de opções. Você verá o **combinar dados** caixa de diálogo.  
  
12. No **combinar dados** caixa de diálogo, clique no botão próximo a **intervalo a ser combinado com dados do MDS** caixa de texto conforme mostrado na imagem a seguir.  
  
     ![Excel - combinar a caixa de diálogo dados](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - combinar a caixa de diálogo de dados")  
  
13. Você deverá ver a caixa de diálogo reduzida agora. Agora, clique em **Planilha2** para alternar para o **Planilha2** guia com os novos dados do fornecedor com 4 linhas (incluindo uma linha de cabeçalho).  
  
14. No **Planilha2**, selecione **todas as linhas, inclusive a linha de cabeçalho** (mesmo se eles parecem já estar selecionada). Você deve ver o **intervalo a ser combinado com dados do MDS** é atualizada automaticamente.  
  
     ![Excel - caixa de diálogo de dados - minimizada de combinar](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - combinar a caixa de diálogo de dados - minimizada")  
  
15. Volte para o **fornecedores** guia sem fechar o **combinar dados** caixa de diálogo.  
  
16. Clique o **botão** lado a **caixa de texto**. Você deverá ver a caixa de diálogo expandida agora. Você deve ver todos os mapeamentos entre as colunas da **Supplier** MDS **entidade** para **Excel** colunas são preenchidas automaticamente.  
  
     ![Excel - combinar preenchida com dados de caixa de diálogo dados](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - combinar preenchida com dados de caixa de diálogo de dados")  
  
17. Certifique-se de que **código** coluna de entidade é mapeada para o **SupplierID** coluna na planilha e **CEP** coluna de entidade é mapeada para o **CEP** coluna na planilha.  
  
18. Sobre o **combinar dados** caixa de diálogo, clique em **combinar**.  
  
19. Confirme se as três linhas de dados foram adicionadas à parte inferior da planilha e devem estar codificadas por cores.  
  
     ![Excel - novos elementos após combinação](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - novos elementos após combinação")  
  
20. Clique em **matemática dados** na faixa de opções para identificar duplicatas. Esse recurso usa a funcionalidade de correspondência do DQS.  
  
21. No **corresponder dados** caixa de diálogo, selecione **fornecedores** para **da Base de dados de conhecimento do DQS**.  
  
     ![Excel - caixa de diálogo comparar dados](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - caixa de diálogo correspondência de dados")  
  
22. Mapeie as colunas da planilha para domínios, conforme mostrado na tabela a seguir.  
  
    |Coluna da planilha|Domínio|  
    |----------------------|------------|  
    |Code (você carregou a Supplier ID como o Code da entidade Supplier no MDS)|ID do Fornecedor|  
    |Name (você carregou o Supplier Name como o Name da entidade Supplier para o MDS)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. Selecione **pré-requisito** para o **código** mapeamento de coluna.  
  
24. Digite **70%** como o **peso** para **Supplier Name** e **30%** como o **peso** para **Contact Email** conforme mostrado na imagem.  
  
25. Clique em **OK**.  
  
26. O processo de correspondência deve identificar uma duplicata para o fornecedor com **código: S1**.  
  
     ![Excel - resultados correspondentes](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - resultados correspondentes")  
  
27. Selecione o **linha duplicada (laranja)**, com o botão direito e clique em **excluir** para excluir a linha.  
  
28. Excluir o **CLUSTER_ID** coluna desde que você não precisa mais.  
  
29. Clique em **publicar** para publicar os outros dois registros novos com **códigos S66** e **S57** no MDS.  
  
30. No **publicar e anotar** caixa de diálogo caixa, adicione um **anotação**e clique em **publicar**.  
  
31. Alterne para o **aplicativo Web Master Data Manager**.  
  
32. Na home page, certifique-se de que **fornecedores** é selecionado para o **modelo**e clique em **Explorer**. Se você já tiver o **Explorer** abra, atualize o navegador da internet.  
  
33. **Classificação** a lista por **código** e procure registros com **S57** e **S66** como códigos. Você também pode usar o **filtro** na barra de ferramentas para procurar um registro específico na lista.  
  
34. Agora, feche **Livro1-Microsoft Excel** janela sem salvar o arquivo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Criando um atributo baseado em domínio no Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  