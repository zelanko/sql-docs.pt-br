---
title: 'Tarefa 2: carregando dados do fornecedor para o MDS usando Suplemento MDS para Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4e3cd4cecd88bcad83c6e9f2a59ecd5f225fb02a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487690"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarefa 2: Carregando dados do fornecedor no MDS usando o Suplemento MDS para Excel
  Nesta tarefa, você publica os dados limpos e de fornecedor no **MDS** usando o **suplemento MDS para Excel**. Você cria uma entidade chamada **Supplier** no modelo **suppliers** criado na lição anterior. A entidade terá um atributo para cada coluna no arquivo do Excel. Os atributos de código e nome da entidade Supplier correspondem às colunas **CódigoDoFornecedor** e **nome do fornecedor** no Excel.  
  
1.  Abra **limpo e com correspondência de suppliers. xls** no **Excel**.  
  
2.  Pressione **Ctrl + a** para selecionar os dados inteiros. É **importante** que você selecione todos os dados na planilha.  
  
3.  Clique em **Dados Mestres** na barra de menus.  
  
4.  Clique no botão **criar entidade** na faixa de faixas.  
  
     ![Excel - Guia Dados Mestre - Botão Criar Entidade](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - Guia Dados Mestre - Botão Criar Entidade")  
  
5.  Na caixa de diálogo **Gerenciar Conexões** , se você não visualizar a conexão com o **servidor MDS local** em **Conexões existentes**, siga este procedimento:  
  
    1.  Selecione **Criar uma nova conexão**e clique no botão **Nova** .  
  
    2.  Na caixa de diálogo **Adicionar nova conexão** , digite **servidor MDS local** para **Descrição** e **http:\//localhost/MDS** para o **endereço do servidor MDS**e clique em **OK** para fechar a caixa de diálogo.  
  
6.  Na caixa de diálogo **gerenciar conexões** , selecione **servidor MDS local** (`http://localhost/MDS`), clique em **testar** para testar a conexão. Clique em **OK** na caixa de mensagem.  
  
7.  Clique em **conectar** para se conectar ao servidor MDS.  
  
8.  Na caixa de diálogo **criar entidade** , selecione **fornecedores** para o **modelo**.  
  
9. Verifique se **VERSION_1** está selecionado para a **versão**.  
  
10. Insira **fornecedor** para o **nome da nova entidade**.  
  
11. Selecione **CódigoDoFornecedor** para **a coluna que contém um campo identificador exclusivo** (você também pode gerar um código automaticamente). Essencialmente, você está mapeando a coluna **CódigoDoFornecedor** no **Excel** para o atributo de **código** da entidade **Supplier** .  
  
12. Selecione **nome do fornecedor** para **a coluna que contém o campo nomes** . Essencialmente, você está mapeando a coluna **nome do fornecedor** no **Excel** para o atributo **nome** da entidade **fornecedor** . Os atributos de **código** e **nome** são atributos obrigatórios para uma entidade no MDS.  
  
     ![Caixa de diálogo Criar Entidade](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Caixa de diálogo Criar Entidade")  
  
13. Clique em **OK** para criar a entidade no MDS, publicar os dados mestre na entidade e fechar a caixa de diálogo **criar entidade** .  
  
14. Agora, você deve ver uma nova planilha chamada **fornecedor**, que é o nome da entidade, adicionada à sua planilha do Excel e, na parte superior da planilha, você verá que a planilha está conectada ao servidor MDS. Observe que a planilha original (intitulada **Plan1**) ainda existe.  
  
     ![Excel - Guias Fornecedor e Planilha1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - Guias Fornecedor e Planilha1")  
  
     ![Excel - Mostrando Detalhes de Conexão do MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - Mostrando Detalhes de Conexão do MDS")  
  
15. Mantenha o **Excel** aberto.  
  
## <a name="next-task"></a>Próxima tarefa  
 [Tarefa 3: Verificando os dados no Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
