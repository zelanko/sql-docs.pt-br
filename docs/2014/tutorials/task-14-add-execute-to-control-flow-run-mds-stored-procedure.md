---
title: 'Tarefa 14: adicionando a tarefa Executar SQL ao fluxo de controle para executar o procedimento armazenado para o MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8c926f2ea3d9ef9973f75764e254c5e0884836e3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177286"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>Tarefa 14: Adicionando a tarefa Executar SQL ao fluxo de controle para executar o procedimento armazenado para MDS
  Depois de carregar dados nas tabelas de preparo do MDS, você executará um procedimento armazenado associado a essa tabela para carregar os dados de preparo nas tabelas adequadas no banco de dados MDS. Esse procedimento armazenado tem dois parâmetros necessários que você precisa passar: LogFlag e VersionName. LogFlag especifica se as transações serão registradas em log durante o processo de preparo e VersionName representa a versão do modelo. Consulte o tópico de [procedimento armazenado em etapas](https://msdn.microsoft.com/library/hh231028.aspx) para obter mais detalhes.

 Nesta tarefa, você adicionará a Tarefa Executar SQL ao fluxo de controle para invocar o procedimento armazenado para carregar os dados preparados nas tabelas adequadas do MDS.

1.  Agora, alterne para a guia **fluxo de controle** .

2.  Arraste e solte a **tarefa Executar SQL** da **caixa de ferramentas do SSIS** para a guia fluxo de **controle** .

3.  Clique com o botão direito do mouse em **Executar tarefa SQL** na guia **fluxo de controle** e clique em **renomear**. Digite **acionar procedimento armazenado para carregar dados no MDS** e pressione **Enter**.

4.  Conecte os **dados de fornecedor de recebimento, limpeza, correspondência e** organização para **disparar o procedimento armazenado para carregar dados** usando o conector verde.

     ![Conectar à tarefa Executar SQL.](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "Conectar à tarefa Executar SQL.")

5.  Usando a janela **variáveis** , adicione duas novas variáveis com as configurações a seguir. Se você não vir a janela **variáveis** , clique em **SSIS** na barra de menus e clique em **variáveis**.

    |Nome|Tipo de Dados|Valor|
    |----------|---------------|-----------|
    |LogFlag|Int32|1|
    |VersionName|String|VERSION_1|

     ![Janela Variáveis do SSIS](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "Janela Variáveis do SSIS")

6.  Clique duas vezes em **disparar procedimento armazenado para carregar dados no MDS**.

7.  Na caixa de diálogo **Editor da tarefa Executar SQL** , selecione **(local). MDS** (ou **localhost. MDS**) para **conexão**.

8.  Digite **exec [STG]. [ udp_Supplier_Leaf]?,?,?** **instrução for SQL**. Você pode verificar o nome usando o SQL Server Management Studio.

     ![Caixa de diálogo Editor de Tarefa Executar SQL - Configurações Gerais](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "Caixa de diálogo Editor de Tarefa Executar SQL - Configurações Gerais")

9. Clique em **mapeamento de parâmetro** no menu à esquerda.

10. Na página **mapeamento de parâmetros** , clique em **Adicionar** para adicionar um mapeamento. Maximize a janela e redimensione as colunas para que você possa visualizar os valores nas listas suspensas corretamente.

11. Selecione **User:: VersionName** na lista suspensa para o **nome da variável**.

12. Selecione **nvarchar** para **tipo de dados**.

13. Digite **0** (zero) para o **nome do parâmetro**.

14. Repita as quatro etapas anteriores para adicionar mais duas variáveis.

    |Nome de variável|Tipo de Dados (importante)|Nome do Parâmetro|
    |-------------------|-----------------------------|--------------------|
    |User::LogFlag|LONG|1|
    |User::BatchTag|NVARCHAR|2|

     ![Editor de Tarefa Executar SQL - Mapeamento de Parâmetros](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "Editor de Tarefa Executar SQL - Mapeamento de Parâmetros")

15. Clique em **OK** para fechar a caixa de diálogo **Executar editor SQL** .

## <a name="next-step"></a>Próxima etapa
 [Tarefa 15: Criando e executando o projeto SSIS](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)


