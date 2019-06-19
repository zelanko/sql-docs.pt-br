---
title: 'Tarefa 1 (pré-requisito): Removendo os dados do fornecedor no MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 84c0acceb4953b819cb5696c4ef90c39e4376846
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481220"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>Tarefa 1 (pré-requisito): Como remover os dados do fornecedor no MDS
  Nesta tarefa, você removerá os dados do fornecedor armazenados no MDS. Você carregou os dados manualmente usando **Suplemento MDS do Excel** na lição anterior. O pacote SSIS que será criado nesta lição carregará automaticamente os dados no MDS para você. Consequentemente, antes de testar o pacote SSIS, será necessário remover os dados do fornecedor do MDS, remover da hierarquia derivada, remover entidades de fornecedor e estado e criar a entidade do fornecedor sem dados.  
  
1.  Inicie **Master Data Manager** navegando até **http://localhost/MDS** ou o site e o aplicativo que você especificou ao configurar o MDS. Se você tiver mantido o **Master Data Manager** aberto, clique em **SQL Server 2012 Master Data Services** na parte superior para alternar para a **home page**.  
  
2.  Clique em **Administração do Sistema** na seção **Tarefas Administrativas** .  
  
3.  Passe o mouse sobre **Gerenciar** no menu e clique em **Hierarquias Derivadas**. É necessário excluir a hierarquia derivada **SuppliersInState** antes de excluir as entidades no modelo **Fornecedores** .  
  
4.  Selecione **SuppliersInState** na lista **Hierarquia Derivada** e clique no botão **X (Excluir)** na barra de ferramentas.  
  
5.  Clique em **OK** para confirmar a exclusão.  
  
6.  Passe o mouse sobre **Gerenciar** no menu e clique em **Entidades**.  
  
7.  Clique em **Supplier** e clique no botão **Excluir (X)** na barra de ferramentas para excluir a entidade. Clique em **OK** nas caixas de mensagem.  
  
8.  Repita a etapa anterior para excluir a entidade **State** .  
  
9. Não feche **Master Data Manager**.  
  
10. Alterne para a janela do Excel que tem o arquivo **Cleansed and Matched Suppliers.xls** aberto. Alterne para a guia **Planilha1** na parte inferior.  
  
11. Selecione apenas a **primeira linha com cabeçalhos**. Não selecione nenhuma outra linha. Você deseja criar as entidades com base nas colunas do Excel, mas não deseja carregar todos os dados. Portanto, selecione apenas a primeira linha com os cabeçalhos.  
  
12. Clique em **Dados Mestres** na barra de menus.  
  
13. Clique em **Criar Entidade** na faixa de opções.  
  
14. Na caixa de diálogo **Gerenciar Conexões** , se você não visualizar a conexão com o **servidor MDS local** em **Conexões existentes**, siga este procedimento:  
  
    1.  Selecione **Criar uma nova conexão**e clique no botão **Nova** .  
  
    2.  Na caixa de diálogo Adicionar nova Conexão, digite **servidor MDS Local** para **descrição** e **http://localhost/MDS** para **endereço do servidor MDS**, e clique em **Okey** para fechar a caixa de diálogo.  
  
15. Na **gerenciar conexões** caixa de diálogo, selecione **servidor MDS Local** (http://localhost/MDS), clique em **testar** para testar a conexão. Clique em **OK** na caixa de mensagem.  
  
16. Clique em **Conectar** para estabelecer uma conexão com o servidor MDS.  
  
17. Na caixa de diálogo **Criar Entidade** , faça o seguinte:  
  
    1.  Confirme se **Intervalo** está definido como **$1:$1**.  
  
    2.  Selecione **Fornecedores** como **Modelo**.  
  
    3.  Selecione **VERSION_1** como **Versão**.  
  
    4.  Digite **Supplier** como **Nome da nova entidade**.  
  
    5.  Selecione **SupplierID** como **Code**.  
  
    6.  Selecione **Supplier Name** como **Nome**.  
  
    7.  Clique em **OK** para criar a entidade e fechar a caixa de diálogo.  
  
18. Feche o **Excel** e **não salve** o arquivo.  
  
19. No **Master Data Manager**, atualize o navegador da Internet e confirme se a entidade **Supplier** é exibida na lista.  
  
20. Alterne para a **home page** clicando em **SQL Server 2012 Master Data Services** na parte superior.  
  
21. Confirme se o modelo **Fornecedores** está selecionado como **Modelo** e **VERSION_1** está selecionada como **Versão**.  
  
22. Clique em **Gerenciador**. Observe que a entidade **Supplier** com todos os atributos foi criada sem **nenhum valor**.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 2 &#40;opcional&#41;: Criando uma exibição de assinatura do MDS usando o Master Data Manager](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  
