---
title: Remover objetos do Data Quality Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f273823825cf94da6269a58389f04207ad1c2707
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68190664"
---
# <a name="remove-data-quality-server-objects"></a>Remover objetos do Data Quality Server
  A desinstalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou a total remoção de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tem o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] não exclui alguns objetos do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , incluindo bancos de dados DQS. Isso implica que você não perca seus dados DQS se desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando a instalação do SQL Server. Exclua manualmente esses objetos do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] quando o processo de desinstalação estiver concluído.  
  
> [!NOTE]
>  -   Antes de desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], considere fazer backup de todas as suas bases de dados de conhecimento exportando-as para um arquivo .dqsb e use o arquivo posteriormente para importar todas as bases de conhecimento em uma nova instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . A exportação e a importação de todas as bases de dados de conhecimento DQS podem ser realizadas somente executando DQSInstaller.exe com os parâmetros de linha de comando apropriados no prompt de comando. Para obter mais informações, consulte [Exportar e importar bases de dados de conhecimento DQS usando o DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).  
> -   Antes de excluir os bancos de dados do DQS, faça backup dos bancos de dados se desejar preservá-los, e use-o posteriormente para restaurar os dados. Para obter informações sobre como fazer isso, consulte [Gerenciar bancos de dados do DQS](../../../2014/data-quality-services/manage-dqs-databases.md).  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>Desinstalar o Data Quality Server de uma instância do SQL Server  
 Se você for apenas desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exclua manualmente os seguintes objetos do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o processo de desinstalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] estiver concluído:  
  
-   Bancos de dados DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA.  
  
-   \##MS_dqs_db_owner_login## and ##MS_dqs_service_login## logins.  
  
-   Procedimento armazenado DQInitDQS_MAIN do banco de dados mestre.  
  
 Você pode excluir estes objetos no SQL Server Management Studio clicando com o botão direito do mouse no objeto e clicando em **Excluir** no menu de atalho.  
  
> [!IMPORTANT]  
>  Se você apenas desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de uma instância do SQL Server usando o parâmetro de linha de comando `-uninstall` no prompt de comando, todos os objetos DQS serão excluídos como parte do processo de desinstalação. Você não precisa excluí-los manualmente após desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. Para desinstalar o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] do prompt de comando, digite o seguinte comando no prompt de comando e pressione ENTER:   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>Desinstalar a instância do SQL Server que contém o Data Quality Server  
 Se você for desinstalar completamente a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tem o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], exclua manualmente os bancos de dados DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA do seu computador depois que o processo de desinstalação for concluído. Para uma instalação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os arquivos dos bancos de dados DQS_MAIN, DQS_PROJECTS e DQS_STAGING_DATA estão disponíveis em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA.  
  
## <a name="see-also"></a>Consulte Também  
 [Desinstalar uma instância existente do SQL Server &#40;instalação&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [Desinstalar o SQL Server 2014](uninstall-sql-server.md)  
  
  
