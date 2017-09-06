---
title: "Gerenciador de Conexão do Excel | Microsoft Docs"
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: a5ce75f3c1715870113626642150028e31a0d58b
ms.contentlocale: pt-br
ms.lasthandoff: 08/17/2017

---
# <a name="excel-connection-manager"></a>Gerenciador de conexões do Excel
  Um gerenciador de conexão do Excel permite a conexão de um pacote a um arquivo de pasta de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel existente. A fonte e o destino do Excel que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usam o gerenciador de conexões do Excel.  
  
 Quando você adiciona um gerenciador de conexões do Excel a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que é resolvido como uma conexão do Excel em tempo de execução, define as propriedades do gerenciador de conexões e o adiciona à coleção **Coleções** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **EXCEL**.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Configuração do gerenciador de conexões do Excel  
 Você pode configurar o gerenciador de conexões do Excel dos seguintes modos:  
  
-   Especificando o caminho do arquivo de pasta de trabalho Excel.  
  
    > [!NOTE]  
    >  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
-   Especificando a versão do Excel que foi usada para criar o arquivo.  
  
-   Indicando se a primeira linha de dados acessados nas planilhas ou intervalos selecionados contém nomes de coluna.  
  
 Se o gerenciador de conexões do Excel for usado por uma origem do Excel, os nomes das colunas serão incluídos junto com os dados extraídos. Se for usado por um destino do Excel, os nomes das colunas serão incluídos nos dados gravados.  
  
 Para obter mais informações sobre o comportamento de fontes e destinos do Excel, consulte [Origem do Excel](../../integration-services/data-flow/excel-source.md) e [Destino do Excel](../../integration-services/data-flow/excel-destination.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
 Para obter informações sobre loop através de um grupo de arquivos do Excel, consulte [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="excel-connection-manager-editor"></a>Editor de Gerenciador de Conexões Excel
  Use a caixa de diálogo **Editor de Gerenciador de Conexões Excel** para adicionar uma conexão a um arquivo da pasta de trabalho novo ou existente do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
 Para saber mais sobre o Gerenciador de Conexões Excel, consulte [Gerenciador de conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Caminho de arquivo do Excel**  
 Digite o caminho e nome de arquivo de um arquivo de pasta de trabalho do Excel (.xls) novo ou existente.  
  
> [!NOTE]  
>  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
> [!WARNING]  
>  O **Editor de Destinos do Excel** cria o arquivo do Excel automaticamente quando você seleciona uma **Conexão do Excel** que aponta para um arquivo novo ou inexistente e, em seguida, clica em **Novo** para **Nome da Folha de Excel**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para navegar até a pasta na qual o arquivo Excel existe ou onde você deseja criar o novo arquivo.  
  
 **Versão do Excel**  
 Especifique a versão do Microsoft Excel que foi usada para criar o arquivo.  
  
 **Primeira linha com nomes de coluna**  
 Especifique se a primeira linha de dados na planilha selecionada contém os nomes de coluna. O valor padrão desta opção é **Verdadeiro**.  
  
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividade para os arquivos do Microsoft Excel e Access
  
Você precisará baixar os componentes de conectividade para arquivos do Microsoft Office se eles ainda não estiverem instalados. Baixar a versão mais recente dos componentes de conectividade para o Excel e acessar arquivos aqui: [redistribuível de 2016 do mecanismo de banco de dados Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes pode abrir arquivos criados por versões anteriores do Excel.

Se o computador tiver uma versão de 32 bits do Office, em seguida, você precisa instalar a versão de 32 bits dos componentes e você também precisa garantir que você execute o pacote no modo de 32 bits.

Se você tiver uma assinatura do Office 365, certifique-se de que você baixe o redistribuível de 2016 do mecanismo de banco de dados de acesso e não o Microsoft Access 2016 Runtime. Quando você executar o instalador, você verá uma mensagem de erro que você não pode instalar a download lado a lado com componentes do Office clique para executar. Para ignorar essa mensagem de erro, execute a instalação no modo silencioso abrindo uma janela de Prompt de comando e executando o. Arquivo EXE baixado com o `/quiet` alternar. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
-   [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
