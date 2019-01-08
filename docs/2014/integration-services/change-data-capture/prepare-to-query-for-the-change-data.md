---
title: Preparar para consultar os dados de alterações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 831e44cb232dea7f0730c73d360cd787f3895878
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756988"
---
# <a name="prepare-to-query-for-the-change-data"></a>Preparar para consultar os dados de alterações
  No fluxo de controle de um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza uma carga incremental de dados de alteração, a terceira e última tarefa servem para consultar as alterações dos dados e adicionar uma tarefa de fluxo de dados.  
  
> [!NOTE]  
>  A segunda tarefa para o fluxo de controle garante que os dados de alteração para o intervalo selecionado estarão prontos. Para obter mais informações sobre essa tarefa, consulte [Determinar se os dados de alteração estão prontos](determine-whether-the-change-data-is-ready.md). Para obter uma descrição do processo geral de criação do fluxo de controle, consulte [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="design-considerations"></a>Considerações de criação  
 Para recuperar os dados de alteração, você chamará uma função com valor de tabela de Transact-SQL que aceita os pontos de extremidade do intervalo como parâmetros de entrada e retorna dados de alteração para o intervalo especificado. Um componente de origem no fluxo de dados chama esta função. Para obter informações sobre esse componente de origem, consulte [Recuperar e compreender os dados de alteração](retrieve-and-understand-the-change-data.md).  
  
 Os componentes de fonte do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usados com mais frequência, incluindo a fonte OLE DB, a fonte ADO e a fonte ADO NET, não podem derivar informações de parâmetros para uma função com valor de tabela. Entretanto, a maioria das fontes não pode chamar uma função parametrizada diretamente.  
  
 Você tem duas opções de design para passar os parâmetros de entrada à função:  
  
-   **Montar a consulta parametrizada como uma cadeia de caracteres**. É possível usar uma tarefa Script ou uma tarefa Executar SQL para montar uma cadeia de caracteres de SQL dinâmica com valores de parâmetro codificados na cadeia de caracteres. Em seguida, essa cadeia de caracteres poderá ser armazenada em uma variável do pacote e usada para definir a propriedade SqlCommand de um componente de origem. Este procedimento é bem-sucedido porque o componente de origem não exige mais as informações do parâmetro.  
  
    > [!NOTE]  
    >  Um script pré-compilado causa menos sobrecarga do que uma tarefa Executar SQL.  
  
-   **Usar um wrapper parametrizado**. Se desejar, você poderá criar um procedimento armazenado parametrizado como um wrapper que chama a função com valor de tabela parametrizada. Este procedimento é bem-sucedido porque o componente de origem pode derivar com êxito as informações de parâmetro para um procedimento armazenado.  
  
 Este tópico usa a primeira opção de design e monta uma consulta parametrizada como uma cadeia de caracteres.  
  
## <a name="preparing-the-query"></a>Preparando a Consulta  
 Antes de concatenar os valores dos parâmetros de entrada em uma cadeia de caracteres simples, é preciso configurar as variáveis do pacote que a consulta precisa.  
  
#### <a name="to-set-up-package-variables"></a>Para definir as variáveis do pacote  
  
-   No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na janela **Variáveis** , crie uma variável com um tipo de dados String para manter a cadeia de caracteres de consulta que retorna da tarefa Executar SQL.  
  
     Este exemplo usa o nome da variável, SqlDataQuery.  
  
 Com a variável de pacote criada, você pode usar tanto uma tarefa Script quanto uma tarefa Executar SQL para concatenar os valores dos parâmetros de entrada. Os dois procedimentos a seguir descrevem como configurar esses componentes.  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>Usar uma tarefa Script para concatenar a cadeia de caracteres de consulta  
  
1.  Na guia **Fluxo de Controle** , adicione uma tarefa Script ao pacote após o contêiner Loop For e conecte o contêiner Loop For à tarefa.  
  
    > [!NOTE]  
    >  Este procedimento assume que o pacote executa uma carga incremental a partir de uma tabela simples. Caso o pacote faça os carregamentos a partir de várias tabelas e tenha um pacote pai com vários pacotes filhos, a tarefa será adicionada como o primeiro componente para cada pacote filho. Para obter mais informações, consulte [Executar uma carga incremental de várias tabelas](perform-an-incremental-load-of-multiple-tables.md).  
  
2.  No **Editor da Tarefa Script**, na página **Script** , selecione as seguintes opções:  
  
    1.  Para **ReadOnlyVariables**, selecione **User::DataReady**, **User::ExtractStartTime**e **User::ExtractEndTime** .  
  
    2.  Para **ReadWriteVariables**, selecione User::SqlDataQuery na lista.  
  
3.  No **Editor da Tarefa Script**, na página **Script** , clique em **Editar Script** para abrir o ambiente de desenvolvimento de script.  
  
4.  No procedimento Principal, digite um dos seguintes segmentos de código:  
  
    -   Se você estiver programando em C#, digite as seguintes linhas de código:  
  
        ```  
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- ou –  
  
    -   Se você estiver programando em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], digite as seguintes linhas de código:  
  
        ```  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  Tire a linha padrão de código que retorna `DtsExecResult.Success` da execução do script.  
  
6.  Feche o ambiente de desenvolvimento de script e o **Editor da Tarefa Script**.  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>Usar uma tarefa Executar SQL para concatenar a cadeia de caracteres de consulta  
  
1.  Na guia **Fluxo de Controle** , adicione uma tarefa Executar SQL ao pacote após o contêiner Loop For e conecte o contêiner Loop For à essa tarefa.  
  
    > [!NOTE]  
    >  Este procedimento assume que o pacote executa uma carga incremental a partir de uma tabela simples. Caso o pacote faça os carregamentos a partir de várias tabelas e tenha um pacote pai com vários pacotes filhos, a tarefa será adicionada como o primeiro componente para cada pacote filho. Para obter mais informações, consulte [Executar uma carga incremental de várias tabelas](perform-an-incremental-load-of-multiple-tables.md).  
  
2.  No **Editor da Tarefa Executar SQL**, na página **Geral** , selecione as seguintes opções:  
  
    1.  Para **Conjunto de Resultados**, selecione **Linha simples**.  
  
    2.  Configure uma conexão válida com o banco de dados fonte.  
  
    3.  Para **SQLSourceType**, selecione **Entrada direta**.  
  
    4.  Para **SQLStatement**, digite a seguinte instrução SQL:  
  
        ```  
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  Neste exemplo, a cláusula `else` gera uma consulta para a carga inicial dos dados de alteração indicando um valor nulo para a data e hora de início. Este exemplo não indica o cenário em que as alterações realizadas antes da captura dos dados de alteração também tenham que ser carregadas para o Data Warehouse.  
  
3.  Na página **Mapeamento de Parâmetros** do **Editor de Tarefa Executar SQL**, faça o seguinte mapeamento:  
  
    1.  Mapeie a variável DataReady para o parâmetro 0.  
  
    2.  Mapeie a variável ExtractStartTime para o parâmetro 1.  
  
    3.  Mapeie a variável ExtractEndTime para o parâmetro 2.  
  
4.  Na página **Conjunto de Resultados** do **Editor de Tarefa Executar SQL**, mapeie o Nome do Resultado para a variável SqlDataQuery.  
  
     O Nome do Resultado é o nome da única coluna que é retornada, SqlDataQuery.  
  
 Os procedimentos anteriores configuram uma tarefa que prepara uma cadeia de caracteres de consulta com valores codificados da cadeia de caracteres para os parâmetros de entrada. O código a seguir é um exemplo de uma cadeia de caracteres de consulta:  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>Adicionando uma tarefa de fluxo de dados  
 A última etapa que projeta o fluxo de controle para o pacote é adicionar uma tarefa de fluxo de dados.  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>Adicionar uma tarefa de fluxo de dados e completar o fluxo de controle  
  
-   Na guia **Fluxo de Controle** , adicione uma tarefa de fluxo de dados e conecte a tarefa que concatenou a cadeia de caracteres de consulta.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de preparar a cadeia de caracteres de consulta e configurar a tarefa de fluxo de dados, a próxima etapa é criar a função com valor de tabela que irá recuperar os dados de alteração do banco de dados.  
  
 **Próximo tópico:** [Criar a função para recuperar os dados de alteração](create-the-function-to-retrieve-the-change-data.md)  
  
  
