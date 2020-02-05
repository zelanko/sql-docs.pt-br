---
title: Conectar-se a uma fonte de dados do Excel (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 82e21333bdd0f4be27f19ee19f43fd5f0abab309
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71285571"
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do Excel (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este artigo mostra como se conectar a uma fonte de dados do **Microsoft Excel** por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server.

A captura de tela a seguir mostra uma conexão de exemplo a uma pasta de trabalho do Microsoft Excel.

![Conexão do Excel](../../integration-services/import-export-data/media/excel-connection.png) 

Talvez seja necessário baixar e instalar arquivos adicionais para se conectar a arquivos do Excel. Para obter mais informações, consulte [Get the files you need to connect to Excel](../load-data-to-from-excel-with-ssis.md#files-you-need) (Obter os arquivos necessários para se conectar ao Excel).

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

## <a name="options-to-specify"></a>Opções a serem especificadas

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o Excel for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

**Caminho de arquivo do Excel**  
 Especifique o nome do arquivo e o caminho completo para o arquivo do Excel. Por exemplo:
-   Para um arquivo no computador local, **C:\\MyData.xlsx**.
-   Para um arquivo em um compartilhamento de rede, **\\\\Sales\\Database\\Northwind.xlsx**.

Se preferir, clique em **Procurar**.  
  
 **Procurar**  
 Localize a planilha usando a caixa de diálogo **Abrir**.  

> [!NOTE]
> O assistente não pode abrir um arquivo do Excel protegido por senha.

 **Versão do Excel**  
Selecione a versão do Excel usada pela pasta de trabalho de origem ou de destino.

**Primeira linha com nomes de coluna**  
Indique se a primeira linha dos dados contém nomes de coluna.
-   Se os dados de origem não contiverem nomes de coluna, mas você habilitar essa opção, o assistente tratará a primeira linha dos dados de origem como os nomes de coluna.
-   Se os dados de origem contiverem nomes de coluna mas você desabilitar essa opção, o assistente tratará a linha de nomes de coluna como a primeira linha de dados.

Se você especificar que os dados não têm nomes de coluna, o assistente usará F1, F2 e assim por diante como títulos de coluna.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Não vejo o Excel na lista de fontes de dados
Se você não vê o Excel na lista de fontes de dados, você está executando o assistente de 64 bits? Os provedores para o Excel e Access são geralmente de 32 bits e não são visíveis no assistente de 64 bits. Em vez disso, execute o Assistente de 32 bits.

> [!NOTE]
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="see-also"></a>Confira também
[Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

