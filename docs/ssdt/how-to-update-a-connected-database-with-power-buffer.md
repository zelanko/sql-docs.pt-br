---
title: 'Como fazer: atualizar um banco de dados conectado com o Power Buffer | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.commitpreview.dialog
ms.assetid: 4048b7f8-71a9-47ad-b812-3fc1e8066240
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9663829f679eeb0c829a94be00c86a7f1e0544af
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098424"
---
# <a name="how-to-update-a-connected-database-with-power-buffer"></a>Como fazer: Atualizar um banco de dados conectado com o Power Buffer
A tecnologia Power Buffer do SQL Server Data Tools facilita a aplicação de alterações em seu banco de dados conectado, armazenando todas as suas edições na sessão atual. Qualquer erro causado ao editar na janela Power Buffer (no Editor Transact\-SQL ou no Designer de Tabela) é exibido imediatamente no painel **Lista de Erros**, permitindo que você siga os erros identificados para a devida solução de problemas. Você pode verificar suas alterações pendentes até estar pronto para aplicá-las no seu banco de dados. Durante o processo de atualização, o SSDT automaticamente cria um script ALTER com base nas suas edições e o alerta para qualquer problema potencial. Você pode aplicar todas as alterações acumuladas em todas as janelas abertas do Power Buffer no mesmo banco de dados, ou salvar o script ALTER para ser implantado posteriormente.  
  
O SSDT também reconhece as alterações feitas em seu esquema de banco de dados fora do Visual Studio. Por exemplo, se você adicionar uma nova tabela a um banco de dados existente no SQL Server Management Studio, essa alteração aparecerá imediatamente no Pesquisador de Objetos do SQL Server no Visual Studio sem precisar atualizá-lo manualmente. O recurso de detecção de descompasso garante que você esteja sempre exibindo a definição de esquema mais recente de um banco de dados no Pesquisador de Objetos do SQL Server. Observe que nenhum objeto de banco de dados aberto no Designer de Tabela ou no Editor Transact\-SQL para edição será atualizado para mostrar alterações fora do Visual Studio.  
  
Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores na seção [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md).  
  
### <a name="to-apply-the-changes-made-in-the-previous-procedures"></a>Para aplicar as alterações feitas nos procedimentos anteriores  
  
1.  Clique no botão verde **Atualizar** na barra de ferramentas (a dica de ferramenta "Atualizar Banco de Dados" será exibida se você passar o mouse sobre o botão). A barra de ferramentas está acima da Grade de Colunas do Designer de Tabela.  
  
2.  A caixa de diálogo **Visualizar Atualizações de Banco de Dados** será exibida. Um script de implantação baseado nas suas alterações é gerado em segundo plano. A caixa de diálogo mostra um resumo das ações que o SSDT vai realizar (por exemplo, criar ou remover entidades de banco de dados), junto com problemas potenciais identificados (isso não se aplica ao nosso procedimento, mas será útil quando sua definição de banco de dados contiver erros que impeçam uma ação de atualização até serem resolvidos).  
  
3.  Se você não desejar atualizar o banco de dados neste momento, clique no botão **Cancelar** para sair da caixa de diálogo **Visualizar Atualizações de Banco de Dados**.  
  
4.  Se você estiver satisfeito com as alterações até o momento, clique no botão **Atualizar Banco de Dados** na caixa de diálogo **Visualizar Atualizações de Banco de Dados**. O script de implantação é executado em seu nome e suas alterações acumuladas agora são aplicadas ao banco de dados.  
  
5.  Se você quiser exibir o script de implantação para verificar ou fazer algumas alterações antes de atualizar, clique no botão **Gerar Script** na caixa de diálogo **Visualizar Atualizações de Banco de Dados**. O script gerado é aberto em uma nova janela do Editor Transact\-SQL. Você pode pressionar o botão **Executar Consulta** na barra de ferramentas do editor Transact\-SQL para executar essa consulta. A ação é similar àquela executada pelo botão **Atualizar Banco de Dados** na Etapa 4.  
  
    > [!WARNING]  
    > Se você fizer qualquer alteração no script de implantação e executá-lo, essas alterações não aparecerão em nenhuma entidade de banco de dados aberta. Por exemplo, se você renomear uma coluna da tabela `Customers` no script de implantação e o executar para atualizar o banco de dados, e a tabela `Customers` estiver aberta no Designer de Tabela, o nome de coluna ainda será o anterior quando você clicou no botão **Atualizar Banco de Dados**. Você tem que fechar o Designer de Tabela manualmente sem salvá-lo localmente como um script. Quando você reabrir a tabela no **Pesquisador de Objetos do SQL Server**, notará que o banco de dados foi realmente atualizado com as alterações feitas no script de implantação.  
  
6.  No painel **Saída** do editor Transact\-SQL (ou no painel **Mensagem**, se você mesmo estiver executando o script de implantação), observe a saída a seguir, que indica que a atualização foi bem-sucedida.  
  
**Criando [dbo].[Customers]...Criando [dbo].[Products]...Criando [dbo].[Suppliers]...Criando FK_Products_SupplierId...Criando FK_Products_CustomerId...Criando CK_Products_ShelfLife A parte transacionada da atualização do banco de dados obteve êxito.Verificando os dados existentes em restrições recém-criadas Atualização concluída.**  
  
7.  No **Pesquisador de Objetos do SQL Server**, observe que as novas tabelas apareceram no nó **Tabelas** do banco de dados **Trade**.  
  
### <a name="to-view-changes-made-to-a-database-outside-visual-studio"></a>Para exibir as alterações feitas em um banco de dados fora do Visual Studio  
  
1.  Abra o SQL Server Management Studio. Na caixa de diálogo **Conectar ao Servidor**, insira o mesmo servidor de banco de dados ao qual você se conectou no Visual Studio e clique em **Conectar**.  
  
2.  No **Pesquisador de Objetos do SQL Server**, expanda **Bancos de dados** e navegue para o banco de dados **Trade**.  
  
3.  Clique com o botão direito em **Tabelas** em **Trade** e selecione **Nova Tabela**. No Designer de Tabela, insira **id** como o Nome da Coluna e **int** como o Tipo de Dados.  
  
4.  Clique no ícone **Salvar** na barra de ferramentas para salvar a tabela. Aceite o nome padrão e clique em **OK**.  
  
    Volte para o Visual Studio. Examine o nó **Tabelas** no banco de dados **Trade** no **Pesquisador de Objetos do SQL Server**. Observe a aparência da tabela **Table_1** criada.  
  
5.  Clique com o botão direito em **Table_1** e selecione **Excluir**. Clique em **Atualizar Banco de Dados** na caixa de diálogo **Visualizar Alterações de Banco de Dados**.  
  
## <a name="see-also"></a>Consulte Também  
[Como: Consertar erros](../ssdt/how-to-fix-errors.md)  
  
