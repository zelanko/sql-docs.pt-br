---
title: Executar um arquivo de script do Reporting Services | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: da90014c17b0540a8bee4e691835361068227565
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814149"
---
# <a name="run-a-reporting-services-script-file"></a>Executar um arquivo de script do Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Os arquivos de script são executados no prompt de comando usando o ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RS.exe). O RS.exe possui diversos argumentos de prompt de comando disponíveis para uso. Para obter mais informações sobre as opções de prompt de comando, consulte [Utilitário RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md). Para obter mais exemplos de script, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="sample-command-lines"></a>Linhas de Comando de Exemplo  
  
-   Execute o Script.rss no ambiente de script designando o servidor de relatório de destino. O Windows Authentication é aplicado por padrão:  
  
    ```  
    rs –i Script.rss -s https://servername/reportserver  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando um nome de usuário e senha para autenticar as chamadas de serviço Web:  
  
    ```  
    rs –i Script.rss -s https://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando um limite do servidor de 30 segundos:  
  
    ```  
    rs –i Script.rss -s https://servername/reportserver -l 30  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando uma variável de script global chamada *report*.  
  
    ```  
    rs –i Script.rss -s https://servername/reportserver -v report="Company Sales"  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando que as operações de serviço Web no arquivo de script sejam executadas como um lote.  
  
    ```  
    rs –i Script.rss -s https://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
