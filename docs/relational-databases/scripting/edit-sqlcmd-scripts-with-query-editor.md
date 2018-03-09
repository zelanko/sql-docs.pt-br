---
title: Editar scripts SQLCMD com o Editor de Consultas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [SQL Server], SQLCMD scripts
- SQLCMD scripts
- modifying scripts
- Query Editor [Database Engine], SQLCMD scripts
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: f77b866d-c330-47c9-9e74-0b8d8dff4b31
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 35f569c6d26c888566eb8dbb47f1472101158d61
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="edit-sqlcmd-scripts-with-query-editor"></a>Editar scripts SQLCMD com o Editor de Consultas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Usando o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode gravar e editar consultas como scripts SQLCMD. Você usa scripts SQLCMD quando precisa processar comandos de Sistema do Windows e instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] no mesmo script.  
  
## <a name="sqlcmd-mode"></a>Modo SQLCMD  
 Para usar o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para gravar ou editar scripts SQLCMD, habilite o modo de script SQLCMD. Por padrão, o modo SQLCMD não é habilitado no Editor de Consultas. Você pode habilitar o modo de script clicando no ícone **Modo SQLCMD** na barra de ferramentas ou selecionando **Modo SQLCMD** no menu **Consulta** .  
  
> [!NOTE]  
>  A habilitação do modo SQLCMD desativa o IntelliSense e o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 No Editor de Consultas, os scripts SQLCMD podem usar os mesmos recursos disponíveis para todos os scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] . Entre esses recursos estão:  
  
-   Codificação por cores  
  
-   Scripts de execução  
  
-   Controle do código-fonte  
  
-   Scripts de análise  
  
-   Showplan  
  
## <a name="enable-sqlcmd-scripting-in-query-editor"></a>Habilitar o script de SQLCMD no Editor de Consultas  
 Para ativar o script SQLCMD em uma janela ativa do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , use o procedimento a seguir.  
  
#### <a name="to-switch-a-database-engine-query-editor-window-to-sqlcmd-mode"></a>Para alternar uma janela do Editor de Consultas do Mecanismo de Banco de Dados para o modo SQLCMD  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e clique em **Nova Consulta**para abrir uma nova janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
2.  No menu **Consulta** , clique em **Modo SQLCMD**.  
  
     O Editor de Consultas executa instruções **sqlcmd** no contexto do Editor de Consultas.  
  
3.  Na barra de ferramentas **Editor do SQL** , na lista **Bancos de Dados Disponíveis** , selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
4.  Na janela do Editor de Consultas, digite as duas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir e a instrução `!!DIR` **sqlcmd** :  
  
    ```  
    SELECT DISTINCT Type FROM Sales.SpecialOffer;  
    GO  
    !!DIR  
    GO  
    SELECT ProductCategoryID, Name FROM Production.ProductCategory;  
    GO  
    ```  
  
5.  Pressione F5 para executar a seção inteira de instruções mistas [!INCLUDE[tsql](../../includes/tsql-md.md)] e MS-DOS.  
  
     Observe os dois painéis de resultados SQL da primeira e terceira instruções.  
  
6.  No painel **Resultados** , clique na guia **Mensagens** para ver as mensagens das três instruções:  
  
    -   (6 linha(s) afetada(s))  
  
    -   \<As informações do diretório>  
  
    -   (4 linha(s) afetada(s))  
  
> [!IMPORTANT]  
>  Quando executado na linha de comando, o utilitário **sqlcmd** permite a interação total com o sistema operacional. Ao usar o Editor de Consultas no **Modo SQLCMD**, tenha cuidado para não executar instruções interativas. O Editor de Consultas não pode responder a prompts do sistema operacional.  
  
 Para obter mais informações sobre como executar o SQLCMD, consulte [sqlcmd Utility](../../tools/sqlcmd-utility.md)ou consulte o tutorial do SQLCMD.  
  
## <a name="enable-sqlcmd-scripting-by-default"></a>Habilitar o script SQLCMD por padrão  
 Para ativar o script de SQLCMD por padrão, no menu **Ferramentas** , selecione **Opções**, expanda **Execução de Consulta**e **SQL Server**, clique na página **Geral** e marque a caixa **Por padrão, abrir novas consultas no modo SQLCMD** .  
  
## <a name="writing-and-editing-sqlcmd-scripts"></a>Gravando e editando scripts SQLCMD  
 Depois de habilitar o modo de script, você pode gravar comandos SQLCMD e instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . As seguintes regras se aplicam:  
  
-   Comandos SQLCMD devem ser a primeira instrução em uma linha.  
  
-   Somente um comando SQLCMD é permitido em cada linha.  
  
-   Comandos SQLCMD podem ser precedidos por comentários ou espaço em branco.  
  
-   Comandos SQLCMD em caracteres de comentário não são executados.  
  
-   Caracteres de comentário de linha única são dois hífens (`--)` ) e devem aparecer no início de uma linha.  
  
-   Comandos de sistema operacional devem ser precedidos por dois pontos de exclamação (`!!`). O comando com dois pontos de exclamação faz com que a instrução que vem depois desses pontos seja executada usando o processador de comando `cmd.exe` . Como o texto depois de `!!` é passado como um parâmetro para `cmd.exe`, a linha de comando final será executada como: `"%SystemRoot%\system32\cmd.exe /c <text after !!>"`.  
  
-   Para fazer uma distinção clara entre comandos SQLCMD e comandos [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os comandos SQLCMD precisam ser precedidos por dois-pontos (`:`).  
  
-   O comando `GO` pode ser usado sem prefácio ou precedido por `!!:`  
  
-   O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] dá suporte para variáveis de ambiente e variáveis definidas como parte de um script SQLCMD, mas não dá suporte para variáveis SQLCMD internas ou **osql** . O processamento SQLCMD feito pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] diferencia maiúsculas de minúsculas para variáveis. Por exemplo, PRINT '$ (COMPUTERNAME)' produz o resultado correto, mas PRINT '$(ComputerName)' retorna um erro.  
  
> [!CAUTION]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SqlClient para a execução em modo regular e SQLCMD. Quando executado na linha de comando, o SQLCMD usa o provedor OLE DB. Devido às diferentes opções padrão que podem ser aplicadas, é possível observar um comportamento diferente ao executar a mesma consulta no Modo SQLCMD do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no utilitário SQLCMD.  
  
## <a name="supported-sqlcmd-syntax"></a>Sintaxe SQLCMD com suporte  
 O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferece suporte às seguintes palavras-chave do script SQLCMD:  
  
 `[!!:]GO[count]`  
  
 `!! <command>`  
  
 `:exit(statement)`  
  
 `:Quit`  
  
 `:r <filename>`  
  
 `:setvar <var> <value>`  
  
 `:connect server[\instance] [-l login_timeout] [-U user [-P password]]`  
  
 `:on error [ignore|exit]`  
  
 `:error <filename>|stderr|stdout`  
  
 `:out <filename>|stderr|stdout`  
  
> [!NOTE]  
>  Para `:error` e `:out`, `stderr` e `stdout` envia a saída à guia de mensagens.  
  
 O Editor de Consultas não oferece suporte aos comandos SQLCMD não listados acima. Na execução de um script que contém palavras-chave SQLCMD sem suporte, o Editor de Consultas enviará uma mensagem "Ignorando comando *\<comando ignorado*>" para o destino de cada palavra-chave sem suporte. O script será executado com êxito, mas os comandos sem suporte serão ignorados.  
  
> [!CAUTION]  
>  Como você não está iniciando o SQLCMD na linha de comando, existem algumas limitações na execução do Editor de Consultas no Modo SQLCMD. Você não pode passar parâmetros de linha de comando como variáveis e, como o Editor de Consultas não tem a capacidade para responder a prompts do sistema operacional, tenha cuidado para não executar instruções interativas.  
  
## <a name="color-coding-in-sqlcmd-scripts"></a>Codificação por cores em scripts SQLCMD  
 Com o script SQLCMD habilitado, os scripts serão codificados por cores. A codificação por cores para palavras-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] permanecerá a mesma. Os comandos SQLCMD são apresentados com um plano de fundo sombreado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa uma instrução **sqlcmd** para criar um arquivo de saída denominado testoutput.txt, executa duas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT juntamente com um comando de sistema operacional (para imprimir o diretório atual). O arquivo resultante contém a saída de mensagem da instrução `DIR` , seguida dos resultados produzidos pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
```  
:out C:\testoutput.txt  
SELECT @@VERSION As 'Server Version'  
!!DIR  
!!:GO  
SELECT @@SERVERNAME AS 'Server Name'  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)  
  
  
