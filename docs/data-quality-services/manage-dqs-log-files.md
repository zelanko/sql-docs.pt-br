---
title: Gerenciar arquivos de log do DQS | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb82238a0e88b3e639a6185bb80de1dd1b33c351
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="manage-dqs-log-files"></a>Gerenciar arquivos de log do DQS
  Arquivos de log do[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) o ajudam a diagnosticar e solucionar problemas no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e no [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. São gerados arquivos de log separados para o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e o [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
 Você pode usar o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para definir a configuração de severidade de log para recursos e módulos do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Adicionalmente, você também pode definir outras configurações (avançadas) para os arquivos de log do DQS, alterando manualmente os parâmetros de configuração de log DQS no banco de dados DQS_MAIN e um arquivo XML no computador [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="DQSServer"></a> Arquivo de log do Servidor Data Quality  
 O arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , DQServerLog.DQS_MAIN.log, inclui logs de atividades que são executadas no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQServerLog.DQS_MAIN.log estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log. O arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] contém as seguintes informações, delimitadas por uma barra (|):  
  
-   Data e hora  
  
-   Nome do thread  
  
-   ID do thread  
  
-   Severidade do log (FATAL, ERROR, WARN, INFO e DEBUG)  
  
    > [!NOTE]  
    >  A severidade de log DEBUG equivale a Detalhado.  
  
-   UID (ID de infraestrutura de DQS interna)  
  
-   Namespace  
  
-   Classe e método  
  
-   Mensagem  
  
 Além disso, o arquivo de log exibe também informações sobre a versão do aplicativo, o nome de computador, o nome do usuário e o sistema operacional.  
  
 Uma entrada de exemplo no arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] tem a seguinte aparência:  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 O arquivo DQServerLog.DQS_MAIN.log é um arquivo rolante; um novo arquivo de log é criado quando o arquivo de log existente excede o limite de tamanho do arquivo rolante especificado nos parâmetros de configuração de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Para obter mais informações, consulte [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="DQSClient"></a> Arquivo de log do Cliente Data Quality  
 O arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , DQClientLog.log, inclui logs do lado do cliente. O arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] está disponível em %APPDATA%\SSDQS\Log. O arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] contém um conjunto de informações semelhante ao do arquivo de log de servidor, mas para o lado do cliente.  
  
 Assim como no arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , o arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] também é um arquivo rolante; um novo arquivo de log é criado quando o arquivo de log existente excede o limite de tamanho do arquivo rolante especificado nos parâmetros de configuração de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Para obter mais informações, consulte [Configure Advanced Settings for DQS Log Files](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="DQSCleansing"></a> Arquivo de log do componente de limpeza DQS  
 O arquivo de log [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] , DQSSSISLog.log, inclui logs de atividades executados usando o [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. O arquivo de log de componente [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] está disponível em %APPDATA%\SSDQS\Log. O arquivo de log [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] contém um conjunto de informações semelhante ao do arquivo de log de servidor, mas para o [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
##  <a name="RT"></a> Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como definir configurações de severidade de log para arquivos de log DQS usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Configurar níveis de severidade para arquivos de log do DQS](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Descreve como definir manualmente configurações avançadas para arquivos de log DQS.|[Definir configurações avançadas para arquivos de log do DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Administração do DQS](../data-quality-services/dqs-administration.md)  
  
  
