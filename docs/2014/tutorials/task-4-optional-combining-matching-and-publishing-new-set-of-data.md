---
title: 'Tarefa 4 (opcional): Combinando, correspondendo e publicando o novo conjunto de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 05c8785427b905138e513ab7134d56def7cdcf4d
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353070"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Tarefa 4 (opcional): Combinando, correspondendo e publicando o novo conjunto de dados
  Com o tempo, você desejará adicionar mais dados ao repositório do MDS. Antes de adicionar dados, ele pode ser útil comparar os novos dados aos dados que já são gerenciados no MDS, para garantir que você não está adicionando dados duplicados ou inexatos. No Suplemento Master Data Services para Excel, você pode combinar dados de duas planilhas e comparar esses dados para identificar e remover duplicatas antes de publicar os dados no MDS. O recurso de correspondência do Suplemento MDS do Excel usa a funcionalidade correspondente do DQS para identificar correspondências nos dados. Nesta tarefa, você combinará dados de duas planilhas em uma e executará a atividade de correspondência para identificar e remover duplicatas antes de publicar no MDS. Ver [correspondência de qualidade de dados em que o suplemento do MDS para Excel](https://msdn.microsoft.com/library/hh548681.aspx) e [combinar dados](https://msdn.microsoft.com/library/hh548680.aspx) tópicos para obter mais detalhes.  
  
1.  Iniciar nova instância do **Excel**. Clique em **começar**, aponte para **execute**, digite **Excel**e clique em **Okey**.  
  
2.  Alterne para o **dados mestres** guia clicando **Master Data** na barra de menus.  
  
3.  Clique em **Connect** na faixa de opções na **conectar e carregar** grupo para se conectar ao **servidor MDS**. Você configurou essa conexão anteriormente nesta lição.  
  
     ![Excel - Mostrar botão Gerenciador em dados mestre](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - Mostrar botão Gerenciador em dados mestre")  
  
4.  Você deve ver a **Master Data Explorer** painel à direita. Se você não vir o Master Data Explorer, clique em **Mostrar Gerenciador** botão na faixa de opções.  
  
5.  No **Master Data Explorer** janela, selecione **fornecedores** na lista suspensa para o **modelo**. Você deve observar que o modelo tem uma entidade: **Fornecedor**.  
  
     ![Excel - janela Master Data Explorer](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - janela Master Data Explorer")  
  
6.  Clique duas vezes em **Supplier** na lista de entidades para carregar os membros da entidade na planilha do Excel.  
  
7.  Clique em **Planilha2** na parte inferior para alternar para o **Planilha2** guia. Se você não vir **Planilha2**, adicione uma nova planilha.  
  
8.  Abra **Suppliers** (o arquivo de entrada original que está incluído nos arquivos do tutorial) de arquivos e copie todas as linhas (três) da **CombineAndCleanse** planilha para **Planilha2**.  
  
9. Volte para o **Supplier** folha na **livro 1 – Microsoft Excel** (não o **Cleansed and Matched Supplier List** Excel) que esteja conectado ao **MDS**.  
  
10. Clique em **Dados Mestres** na barra de menus.  
  
11. Clique em **combinar dados** na faixa de opções. Você verá a **combinar dados** caixa de diálogo.  
  
12. No **combinar dados** diálogo caixa, clique no botão próximo a **intervalo a ser combinado com dados do MDS** caixa de texto, conforme mostrado na imagem a seguir.  
  
     ![Excel - combinar dados caixa de diálogo](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - combinar caixa de diálogo de dados")  
  
13. Você deverá ver a caixa de diálogo reduzida agora. Agora, clique em **Planilha2** para alternar para o **Planilha2** guia que tem os novos dados do fornecedor com 4 linhas (incluindo uma linha de cabeçalho).  
  
14. No **Planilha2**, selecione **todas as linhas, incluindo a linha de cabeçalho** (mesmo se eles parecem já estar selecionada). Você deve ver a **intervalo a ser combinado com dados do MDS** é atualizada automaticamente.  
  
     ![Excel - caixa de diálogo de dados - minimizada de combinar](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - caixa de diálogo de dados - minimizada de combinar")  
  
15. Volte para o **fornecedores** guia sem fechar o **combinar dados** caixa de diálogo.  
  
16. Clique o **botão** ao lado de **caixa de texto**. Você deverá ver a caixa de diálogo expandida agora. Você deve ver todos os mapeamentos entre colunas do **Supplier** MDS **entidade** para **Excel** colunas são preenchidas automaticamente.  
  
     ![Excel - preenchida com dados de caixa de diálogo dados de combinar](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - combinar preenchida com dados de caixa de diálogo de dados")  
  
17. Certifique-se de que **código** entidade é mapeada para o **SupplierID** coluna na planilha e **CEP** entidade é mapeada para o **CEP** coluna na planilha.  
  
18. Sobre o **combinar dados** caixa de diálogo, clique em **combinar**.  
  
19. Confirme se as três linhas de dados foram adicionadas à parte inferior da planilha e devem estar codificadas por cores.  
  
     ![Excel - novos elementos após combinação](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - novos elementos após combinação")  
  
20. Clique em **matemática dados** na faixa de opções para identificar duplicatas. Esse recurso usa a funcionalidade de correspondência do DQS.  
  
21. No **corresponder dados** caixa de diálogo, selecione **fornecedores** para **da Base de dados de conhecimento do DQS**.  
  
     ![Excel - caixa de diálogo de dados de correspondência](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - caixa de diálogo de dados de correspondência")  
  
22. Mapeie as colunas da planilha para domínios, conforme mostrado na tabela a seguir.  
  
    |Coluna da planilha|Domínio|  
    |----------------------|------------|  
    |Code (você carregou a Supplier ID como o Code da entidade Supplier no MDS)|ID do Fornecedor|  
    |Name (você carregou o Supplier Name como o Name da entidade Supplier para o MDS)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. Selecione **pré-requisito** para o **código** mapeamento de coluna.  
  
24. Insira **70%** como o **peso** para **Supplier Name** e **30%** como o **peso** para **Contact Email** conforme mostrado na imagem.  
  
25. Clique em **OK**.  
  
26. O processo de correspondência deve identificar uma duplicata para o fornecedor com **Código: S1**.  
  
     ![Excel - resultados correspondentes](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - resultados correspondentes")  
  
27. Selecione o **linha duplicada (laranja)**, clique com botão direito e clique em **excluir** para excluir a linha.  
  
28. Excluir o **CLUSTER_ID** coluna, pois você não precisa mais.  
  
29. Clique em **Publish** para publicar os outros dois novos registros com **códigos S66** e **S57** no MDS.  
  
30. No **publicar e anotar** diálogo caixa, adicione um **anotação**e clique em **publicar**.  
  
31. Alterne para o **aplicativo Web Master Data Manager**.  
  
32. Na home page, certifique-se de que **fornecedores** está selecionado para o **modelo**e clique em **Explorer**. Se você já tiver o **Explorer** aberto, atualize o navegador da internet.  
  
33. **Classificar** a lista por **código** e procure registros com **S57** e **S66** como códigos. Você também pode usar o **filtro** na barra de ferramentas para procurar um registro específico na lista.  
  
34. Agora, feche **Book1 - Microsoft Excel** janela sem salvar o arquivo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Criando um atributo baseado em domínio no Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
