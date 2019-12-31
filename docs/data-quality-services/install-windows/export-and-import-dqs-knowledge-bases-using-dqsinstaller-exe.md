---
title: Export and Import DQS Knowledge Bases Using DQSInstaller.exe
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: bb2f2a1a1e6aa9b63478b95d7f802e3df7cd127c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254777"
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Export and Import DQS Knowledge Bases Using DQSInstaller.exe

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Para uma instalação existente do DQS, você pode exportar de uma só vez todas as bases de dados de conhecimento de seu [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] para um arquivo de backup DQS (.dqsb) e, depois, usar o arquivo .dqsb para importar todas as bases de dados de conhecimento de uma só vez para um [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] diferente, executando o arquivo DQSInstaller.exe no prompt de comando. Para obter mais informações sobre a execução de DQSInstaller.exe do prompt de comando, consulte [Executar o DQSInstaller.exe do prompt de comando](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) em [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
 Este recurso lhe permite fazer um backup de *todas* as bases de dados de conhecimento no [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de uma só vez, sem precisar exportar individualmente cada base de dados de conhecimento para um arquivo .dqs usando o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Da mesma forma, você pode importar *todas* as bases de dados de conhecimento do arquivo de backup para outro [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de uma só vez, sem precisar importar cada base de dados de conhecimento individualmente de um arquivo .dqs usando o [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]. Isso é particularmente útil ao fazer backup e restaurar suas bases de dados de conhecimento quando você está desinstalando o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] em um computador, e reinstalando-o em outro computador. Você pode exportar facilmente todas as bases de dados de conhecimento em uma instalação existente do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] para um arquivo de backup DQS (.dqsb) e, depois importar todas as bases de dados de conhecimento do arquivo de backup após instalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] em outro computador.  
  
##  <a name="export"></a>Exportando bases de dados de conhecimento para arquivo. dqsb  
 Você pode exportar todas as bases de dados de conhecimento do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] existente a qualquer momento, ou durante a desinstalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].  
  
-   Para exportar todas as bases de dados de conhecimento em um [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] para um arquivo de backup DQS (.dqsb), execute o DQSInstaller.exe com o parâmetro `exportkbs` do prompt de comando, junto com o caminho completo e o nome de arquivo para onde você deseja exportar as bases de dados de conhecimento. Por exemplo, para exportar todas as bases de dados de conhecimento para o arquivo DQSBackup.dqsb na unidade C:  
  
    ```  
    dqsinstaller.exe -exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Se o nome de arquivo fornecido já existir no local especificado, o instalador o solicitará se o arquivo deve ser substituído.  
  
-   Para exportar todas as bases de dados de conhecimento para um arquivo de backup DQS ao desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], execute o DQSInstaller.exe com o parâmetro `uninstall` do prompt de comando, junto com o caminho completo e o nome de arquivo para onde deseja exportar as bases de dados de conhecimento. Por exemplo, para exportar todas as bases de dados de conhecimento para o arquivo DQSBackup.dqsb na unidade C:, e depois desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]:  
  
    ```  
    dqsinstaller.exe -uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Se você não especificar o caminho completo e o nome do arquivo de backup DQS durante a desinstalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] no prompt de comando usando o parâmetro `uninstall` , uma mensagem será exibida indicando que todas as bases de dados de conhecimento serão excluídas, e permitindo que você decida se deseja continuar com o processo de desinstalação.  
  
##  <a name="import"></a>Importando bases de dados de conhecimento do arquivo. dqsb  
 Você pode importar todas as bases de dados de conhecimento de um arquivo de backup DQS (.dqsb) após concluir a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Para importar bases de dados de conhecimento, você deve ter um arquivo de backup DQS válido (.dqsb).  
  
 Execute o arquivo DQSInstaller.exe com o parâmetro `importkbs` do prompt de comando, junto com o caminho completo e o nome de arquivo de onde deseja importar as bases de dados de conhecimento. Por exemplo, para importar todas as bases de dados de conhecimento do arquivo DQSBackup.dqsb na unidade C:  
  
```  
dqsinstaller.exe -importkbs c:\DQSBackup.dqsb  
```  
  
 Se existirem bases de dados de conhecimento em seu [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] com o mesmo nome que aquelas importadas, os nomes das bases de dados de conhecimento importadas serão anexados com um sublinhado (_) seguido de um valor inteiro, começando em 1. Por exemplo, se o domínio "CompanyName" for duplicado, o nome de domínio importado será "CompanyName_1".  
  
## <a name="see-also"></a>Consulte Também  
 [Executar o DQSInstaller. exe para concluir a instalação do Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Exportar uma base de dados de conhecimento para um arquivo. DQS](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [Importar uma base de dados de conhecimento de um arquivo. DQS](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
