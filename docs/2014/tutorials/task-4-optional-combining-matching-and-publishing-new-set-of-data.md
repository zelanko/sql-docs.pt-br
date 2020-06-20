---
title: 'Tarefa 4 (opcional): combinação, correspondência e publicação de novo conjunto de dados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d2f67c88be66be069a48d008ba6889a81dfda8ae
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061111"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Tarefa 4 (Opcional): Combinando, correspondendo e publicando o novo conjunto de dados
  Com o tempo, você desejará adicionar mais dados ao repositório do MDS. Antes de adicionar dados, pode ser útil comparar os novos dados com os dados que já são gerenciados no MDS, para garantir que você não esteja adicionando dados duplicados ou imprecisos. No Suplemento Master Data Services para Excel, você pode combinar dados de duas planilhas e comparar esses dados para identificar e remover duplicatas antes de publicar os dados no MDS. O recurso de correspondência do Suplemento MDS do Excel usa a funcionalidade correspondente do DQS para identificar correspondências nos dados. Nesta tarefa, você combinará dados de duas planilhas em uma e executará a atividade de correspondência para identificar e remover duplicatas antes de publicar no MDS. Consulte [correspondência de qualidade de dados nos tópicos suplemento MDS para Excel](https://msdn.microsoft.com/library/hh548681.aspx) e [combinar dados](https://msdn.microsoft.com/library/hh548680.aspx) para obter mais detalhes.  
  
1.  Inicie a nova instância do **Excel**. Clique em **Iniciar**, aponte para **executar**, digite **Excel**e clique em **OK**.  
  
2.  Alterne para a guia **dados mestres** clicando em **dados mestres** na barra de menus.  
  
3.  Clique em **conectar** na faixa de **-se no grupo conectar e carregar** para se conectar ao **servidor MDS**. Você configurou essa conexão anteriormente nesta lição.  
  
     ![Excel - Mostrar Botão do Explorer na guia Dados Mestre](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - Mostrar Botão do Explorer na guia Dados Mestre")  
  
4.  Você deve ver o painel de **Data Explorer mestre** à direita. Se você não vir o Data Explorer mestre, clique no botão **Mostrar Explorer** na faixa de faixas.  
  
5.  Na janela de **Data Explorer mestre** , selecione **fornecedores** na lista suspensa para o **modelo**. Você verá que o modelo tem uma entidade: **fornecedor**.  
  
     ![Excel - Janela Master Data Explorer](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - Janela Master Data Explorer")  
  
6.  Clique duas vezes em **fornecedor** na lista de entidades para carregar os membros da entidade na planilha do Excel.  
  
7.  Clique em **Planilha2** na parte inferior para alternar para a guia **Planilha2** . Se você não vir a **Planilha2**, adicione uma nova planilha.  
  
8.  Abra **Suppliers.xls** arquivo (o arquivo de entrada original que está incluído nos arquivos do tutorial) e copie todas as (três) linhas da planilha **CombineAndCleanse** para **Planilha2**.  
  
9. Volte para a planilha de **fornecedores** no **livro 1-Microsoft Excel** (não o Excel de lista de fornecedores com **limpeza e correspondência** ) que está conectado ao **MDS**.  
  
10. Clique em **Dados Mestres** na barra de menus.  
  
11. Clique em **combinar dados** na faixa de faixas. Você verá a caixa de diálogo **combinar dados** .  
  
12. Na caixa de diálogo **combinar dados** , clique no botão ao lado da caixa **de texto intervalo a ser combinado com dados do MDS** , conforme mostrado na imagem a seguir.  
  
     ![Excel - Caixa de diálogo Combinar Dados](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - Caixa de diálogo Combinar Dados")  
  
13. Você deverá ver a caixa de diálogo reduzida agora. Agora, clique em **Planilha2** para alternar para a guia **Planilha2** que tem os novos dados de fornecedor com 4 linhas (incluindo uma linha de cabeçalho).  
  
14. Na **Planilha2**, selecione **todas as linhas, incluindo a linha de cabeçalho** (mesmo que pareçam já estar selecionadas). Você deve ver o **intervalo a combinar com dados do MDS** é atualizado automaticamente.  
  
     ![Excel - Caixa de diálogo Combinar Dados - minimizada](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - Caixa de diálogo Combinar Dados - minimizada")  
  
15. Volte para a guia **fornecedores** sem fechar a caixa de diálogo **combinar dados** .  
  
16. Clique no **botão** ao lado da **caixa de texto**. Você deverá ver a caixa de diálogo expandida agora. Você deve ver que todos os mapeamentos entre colunas da **entidade** do **fornecedor** MDS para colunas do **Excel** são populados automaticamente.  
  
     ![Excel - Caixa de diálogo Combinar Dados - preenchida com dados](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - Caixa de diálogo Combinar Dados - preenchida com dados")  
  
17. Verifique se a coluna de entidade de **código** está mapeada para a coluna **CódigoDoFornecedor** na planilha e a coluna de entidade **CEP** está mapeada para a coluna **CEP** na planilha.  
  
18. Na caixa de diálogo **combinar dados** , clique em **combinar**.  
  
19. Confirme se as três linhas de dados foram adicionadas à parte inferior da planilha e devem estar codificadas por cores.  
  
     ![Excel - Novos elementos após combinação](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - Novos elementos após combinação")  
  
20. Clique em **dados matemáticos** na faixa de faixas para identificar duplicatas. Esse recurso usa a funcionalidade de correspondência do DQS.  
  
21. Na caixa de diálogo **corresponder dados** , selecione **fornecedores** para a **base de dados de conhecimento do DQS**.  
  
     ![Excel - Caixa de diálogo Corresponder Dados](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - Caixa de diálogo Corresponder Dados")  
  
22. Mapeie as colunas da planilha para domínios, conforme mostrado na tabela a seguir.  
  
    |Coluna da planilha|Domínio|  
    |----------------------|------------|  
    |Code (você carregou a Supplier ID como o Code da entidade Supplier no MDS)|ID do Fornecedor|  
    |Name (você carregou o Supplier Name como o Name da entidade Supplier para o MDS)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. Selecione **pré-requisito** para o mapeamento de coluna de **código** .  
  
24. Insira **70%** como o **peso** do **nome do fornecedor** e **30%** como o **peso** do **email de contato** , conforme mostrado na imagem.  
  
25. Clique em **OK**.  
  
26. O processo de correspondência deve identificar uma duplicata para o fornecedor com **código: S1**.  
  
     ![Excel - Resultados de Correspondência](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - Resultados de Correspondência")  
  
27. Selecione a **linha duplicada (laranja)**, clique com o botão direito do mouse e clique em **excluir** para excluir a linha.  
  
28. Exclua a coluna **CLUSTER_ID** , pois você não precisa mais dela.  
  
29. Clique em **publicar** para publicar os outros dois novos registros com os **códigos S66** e **s57** para MDS.  
  
30. Na caixa de diálogo **publicar e anotar** , adicione uma **anotação**e clique em **publicar**.  
  
31. Alterne para o **aplicativo Web Master Data Manager**.  
  
32. Na home page, verifique se **fornecedores** está selecionado para o **modelo**e clique em **Gerenciador**. Se você já tiver o **Gerenciador** aberto, atualize o navegador da Internet.  
  
33. **Classifique** a lista por **código** e procure por registros com **s57** e **S66** como códigos. Você também pode usar o botão **Filtrar** na barra de ferramentas para procurar um registro específico na lista.  
  
34. Agora, feche a janela **book1-Microsoft Excel** sem salvar o arquivo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Criando um atributo baseado em domínio no Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
