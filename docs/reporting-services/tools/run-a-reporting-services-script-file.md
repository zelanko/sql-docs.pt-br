---
title: Executar um arquivo de Script do Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ed67f96cd8487703e81ec702505724725e5c13d3
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="run-a-reporting-services-script-file"></a>Executar um arquivo de script do Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Os arquivos de script são executados no prompt de comando usando o ambiente de script do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RS.exe). O RS.exe possui diversos argumentos de prompt de comando disponíveis para uso. Para obter mais informações sobre as opções de prompt de comando, consulte [Utilitário RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md). Para obter mais exemplos de script, consulte [Amostras de produto do SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="sample-command-lines"></a>Linhas de Comando de Exemplo  
  
-   Execute o Script.rss no ambiente de script designando o servidor de relatório de destino. O Windows Authentication é aplicado por padrão:  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando um nome de usuário e senha para autenticar as chamadas de serviço Web:  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando um limite do servidor de 30 segundos:  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -l 30  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando uma variável de script global chamada *report*.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -v report="Company Sales"  
    ```  
  
-   Execute o Script.rss no ambiente de script especificando que as operações de serviço Web no arquivo de script sejam executadas como um lote.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
