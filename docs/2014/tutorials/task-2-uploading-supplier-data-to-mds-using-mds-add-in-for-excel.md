---
title: 'Tarefa 2: Enviar dados do fornecedor para MDS usando o Complemento mds para Excel | Microsoft Docs'
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487690"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarefa 2: Carregando dados do fornecedor no MDS usando o Suplemento MDS para Excel
  Nesta tarefa, você publica os dados limpos e do fornecedor para **MDS** usando o **Complemento MDS para Excel**. Você cria uma entidade chamada **Fornecedor** no modelo **Fornecedores** que você criou na aula anterior. A entidade terá um atributo para cada coluna no arquivo do Excel. Os atributos de Código e Nome da entidade Fornecedor correspondem às colunas **SupplierID** e **Supplier Name** no Excel.  
  
1.  Abra **fornecedores limpos e combinados.xls** no **Excel**.  
  
2.  Pressione **CTRL+A** para selecionar dados inteiros. É **importante** que você selecione todos os dados na planilha.  
  
3.  Clique em **Dados Mestres** na barra de menus.  
  
4.  Clique no botão **Criar entidade** na fita.  
  
     ![Excel - Guia Dados Mestre - Botão Criar Entidade](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - Guia Dados Mestre - Botão Criar Entidade")  
  
5.  Na caixa de diálogo **Gerenciar Conexões** , se você não visualizar a conexão com o **servidor MDS local** em **Conexões existentes**, siga este procedimento:  
  
    1.  Selecione **Criar uma nova conexão**e clique no botão **Nova** .  
  
    2.  Na caixa de diálogo **Adicionar nova conexão,** digite **O Servidor MDS local** para **descrição** e **http:\//localhost/MDS** for **MDS server address**e clique em **OK** para fechar a caixa de diálogo.  
  
6.  Na caixa de diálogo **Gerenciar conexões,** `http://localhost/MDS`selecione Servidor **MDS local** ( ), clique em **Testar** para testar a conexão. Clique em **OK** na caixa de mensagem.  
  
7.  Clique **em Conectar-se** ao servidor MDS.  
  
8.  Na caixa de diálogo **Criar entidade,** selecione **Fornecedores** para o **Modelo**.  
  
9. Certifique-se de que **VERSION_1** está selecionada para **versão**.  
  
10. Digite **Fornecedor** para **Novo nome de entidade**.  
  
11. Selecione **SupplierID** para a coluna que contém um campo **identificador exclusivo** (você também pode gerar um código automaticamente). Você está essencialmente mapeando a coluna **SupplierID** no **Excel** para o atributo **Código** da entidade **fornecedora.**  
  
12. Selecione **Nome do fornecedor** para a coluna que contém o campo **nomes.** Você está essencialmente mapeando a coluna **Nome do Fornecedor** no **Excel** para o atributo **Nome** da entidade **Fornecedor.** Os atributos **Código** e **Nome** são atributos obrigatórios para uma entidade em MDS.  
  
     ![Caixa de diálogo Criar Entidade](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Caixa de diálogo Criar Entidade")  
  
13. Clique em **OK** para criar a entidade no MDS, publique os dados mestres para a entidade e feche a caixa de diálogo **Criar entidade.**  
  
14. Agora, você deve ver uma nova folha intitulada **Fornecedor**, que é o nome da entidade, adicionada à sua planilha excel e no topo da planilha você deve ver que a planilha está conectada ao servidor MDS. Observe que a planilha original (intitulada **Folha1**) ainda existe.  
  
     ![Excel - Guias Fornecedor e Planilha1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - Guias Fornecedor e Planilha1")  
  
     ![Excel - Mostrando Detalhes de Conexão do MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - Mostrando Detalhes de Conexão do MDS")  
  
15. Mantenha **o Excel** aberto.  
  
## <a name="next-task"></a>Próxima tarefa  
 [Tarefa 3: Verificando os dados no Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
