---
title: "Conectar a uma fonte de dados do Excel (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d744e84aa2b4ae0462a5d5a1e4453a9e86abb890
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

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
> Talvez seja necessário baixar e instalar arquivos adicionais para se conectar à versão do Excel selecionada. Consulte [obter os arquivos necessários para se conectar ao Excel](#officeDownloads) nesta página para obter mais informações.

Se você tiver um problema quando você especificar uma versão, tente especificar uma versão diferente, até mesmo uma versão anterior. Por exemplo, você pode não ser capaz de instalar os provedores de dados do Office 2016, porque você tem uma assinatura do Microsoft Office 365. Você só pode instalar os provedores de dados para Excel 2016 e acesso 2016 com uma versão de área de trabalho do Microsoft Office. Nesse caso, você pode especificar o Excel 2013 em vez do Excel 2016. As duas versões do provedor são funcionalmente equivalentes. Essa limitação de tempo de execução do Office 2016 é mencionada na [esta postagem de blog](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

**Primeira linha com nomes de coluna**  
Indique se a primeira linha de dados contém nomes de coluna.
-   Se os dados não contêm nomes de coluna, mas você habilitar essa opção, o assistente trata a primeira linha da fonte de dados como os nomes de coluna.
-   Se os dados contém nomes de coluna, mas você desabilitar essa opção, o assistente trata a linha de nomes de coluna como a primeira linha de dados.

Se você especificar que os dados não tem nomes de coluna, o assistente usa F1, F2 e assim por diante, como cabeçalhos de coluna.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Não vejo Excel na lista de fontes de dados
Se você não vir o Excel na lista de fontes de dados, você está executando o Assistente de 64 bits? Os provedores para o Excel e Access são geralmente de 32 bits e não são visíveis no Assistente de 64 bits. Execute o Assistente de 32 bits em vez disso.

## <a name="officeDownloads"></a>Obter os arquivos que necessários para se conectar ao Excel  
Você precisará baixar os componentes de conectividade para fontes de dados do Microsoft Office, incluindo o Excel e Access, se eles ainda não estiverem instalados.

As versões mais recentes dos componentes podem abrir arquivos criados em versões anteriores dos programas. Em alguns casos, as versões anteriores dos componentes também podem abrir arquivos criados por versões mais recentes dos programas. Por exemplo, se você não pode instalar os componentes do Office 2016, use os componentes do Office 2013. As duas versões do provedor são funcionalmente equivalentes. Essa limitação de tempo de execução do Office 2016 é mencionada na [esta postagem de blog](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

Se o computador tem uma versão de 32 bits do Office, isso é normal, mesmo em computadores de 64 bits, você precisa instalar a versão de 32 bits dos componentes. Você também precisa garantir que você execute o Assistente de 32 bits ou executa o pacote de atualização do SQL Server Integration Services que o assistente cria no modo de 32 bits. 
 
|Versão do Microsoft Office|Download|  
|------------------------------|--------------|  
|2016|[Tempo de execução do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Tempo de execução do Microsoft Access 2013](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Tempo de execução do Microsoft Access 2010](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System Driver: componentes de conectividade de dados](https://www.microsoft.com/download/details.aspx?id=23734)|  

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


