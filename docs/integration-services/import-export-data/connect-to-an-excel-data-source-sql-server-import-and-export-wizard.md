---
title: "Conectar a uma fonte de dados do Excel (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b4411fdd2337d93f15b149febf845fb7b0762c40
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados do Excel (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **Microsoft Excel** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server.

A captura de tela a seguir mostra uma conexão de exemplo a uma pasta de trabalho do Microsoft Excel.

![Conexão do Excel](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>Opções para especificar

> [!NOTE]
> As opções de conexão para este provedor de dados são os mesmos se o Excel é sua fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

**Caminho de arquivo do Excel**  
 Especifique o nome de arquivo e caminho para o arquivo do Excel. Por exemplo:
-   Para um arquivo no computador local, **c:\\MyData.xlsx**.
-   Para um arquivo em um compartilhamento de rede,  **\\ \\vendas\\banco de dados\\Northwind.xlsx**.

Se preferir, clique em **Procurar**.  
  
 **Procurar**  
 Localize a planilha usando a caixa de diálogo **Abrir**.  

> [!NOTE]
> O assistente não pode abrir um arquivo do Excel protegido por senha.

 **Versão do Excel**  
Selecione a versão do Excel usada pela pasta de trabalho de origem.

> [!IMPORTANT]
> Você precisará baixar e instalar arquivos adicionais para conectar-se aos arquivos do Excel. Consulte [obter os arquivos necessários para se conectar ao Excel](#officeDownloads) nesta página para obter mais informações.

**Primeira linha com nomes de coluna**  
Indique se a primeira linha de dados contém nomes de coluna.
-   Se os dados não contêm nomes de coluna, mas você habilitar essa opção, o assistente trata a primeira linha da fonte de dados como os nomes de coluna.
-   Se os dados contém nomes de coluna, mas você desabilitar essa opção, o assistente trata a linha de nomes de coluna como a primeira linha de dados.

Se você especificar que os dados não tem nomes de coluna, o assistente usa F1, F2 e assim por diante, como cabeçalhos de coluna.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Não vejo Excel na lista de fontes de dados
Se você não vir o Excel na lista de fontes de dados, você está executando o Assistente de 64 bits? Os provedores para o Excel e Access são geralmente de 32 bits e não são visíveis no Assistente de 64 bits. Execute o Assistente de 32 bits em vez disso.

> [!NOTE]
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="officeDownloads"></a>Obter os arquivos que necessários para se conectar ao Excel  
Você precisará baixar os componentes de conectividade para fontes de dados do Microsoft Office, incluindo o Excel e Access, se eles ainda não estiverem instalados. Baixar a versão mais recente dos componentes de conectividade para o Excel e acessar arquivos aqui: [redistribuível de 2016 do mecanismo de banco de dados Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes pode abrir arquivos criados por versões anteriores do Excel.

Se o computador tiver uma versão de 32 bits do Office, em seguida, você precisa instalar a versão de 32 bits dos componentes e você também precisa garantir que você execute o pacote no modo de 32 bits.

Se você tiver uma assinatura do Office 365, certifique-se de que você baixe o redistribuível de 2016 do mecanismo de banco de dados de acesso e não o Microsoft Access 2016 Runtime. Quando você executar o instalador, você verá uma mensagem de erro que você não pode instalar a download lado a lado com componentes do Office clique para executar. Para ignorar essa mensagem de erro, execute a instalação no modo silencioso abrindo uma janela de Prompt de comando e executando o. Arquivo EXE baixado com o `/quiet` alternar. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


