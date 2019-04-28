---
title: Atualizar assemblies SQLCLR após atualizar o .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b1a008cc-7e6b-4655-a869-bd429f986400
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ee3e777d517558f09a8edad35ed8bbc68a53d9cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792467"
---
# <a name="upgrade-sqlclr-assemblies-after-net-framework-update"></a>Atualizar assemblies SQLCLR após atualizar o .NET Framework
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] O DQS é uma coleção de rotinas SQLCR (SQL Common Language Runtime) que fazem referência aos assemblies do Microsoft .NET Framework 4. Quando você instala qualquer atualização do .NET Framework em seu computador que afete qualquer assembly do .NET Framework referenciado, isso leva a uma alteração na MVID (ID da Versão do Módulo) do assembly no GAC (Cache de Assembly Global). Isso causa uma incompatibilidade entre as MVIDs do assembly referenciado no GAC e o assembly no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se a atualização do .NET Framework exigir que você reinicie o computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , os assemblies do SQLCLR afetados serão atualizados automaticamente para corrigir o problema de incompatibilidade do MVID ao reiniciar o computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Porém, para as atualizações do .NET Framework que não exigem que você reinicie seu computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , um erro ocorre devido à incompatibilidade nos MVIDs dos assemblies quando você tenta se conectar a um [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] usando um [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]:  
  
```  
A new version of .NET was installed on this machine. In order to continue to work with DQS please run dqsinstaller.exe -upgradedlls.  
```  
  
 Para corrigir este problema, os assemblies SQLCLR afetados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] devem ser atualizados. Você pode fazer isso executando o arquivo DQSInstaller.exe com o parâmetro de linha de comando **upgradedlls** para ignorar a recriação dos bancos de dados DQS e atualizar apenas os assemblies afetados. Isso garante que sua base de conhecimento, projetos de qualidade de dados e quaisquer outros dados no DQS sejam preservados.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve estar conectado como um membro do grupo Administradores no computador do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa sysadmin na instância do SQL Server em que o [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] está instalado.  
  
### <a name="to-upgrade-sqlclr-assemblies"></a>Para atualizar assemblies SQLCLR  
  
1.  Iniciar o prompt de comando.  
  
2.  Ao prompt de comando, altere seu diretório ao local onde DQSInstaller.exe está disponível. Se você instalou a instância padrão do SQL Server, o arquivo DQSInstaller.exe estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  No prompt de comando, digite o seguinte comando e pressione ENTER:  
  
    ```  
    dqsinstaller.exe -upgradedlls  
    ```  
  
4.  As outras etapas são iguais às etapas 2 a 6 na seção [Executar o DQSInstaller.exe na tela Iniciar, no menu Iniciar ou no Windows Explorer](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer) em [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Data Quality Services](install-data-quality-services.md)   
 [Atualize o esquema de bancos de dados DQS depois de instalar a atualização do SQL Server](upgrade-dqs-databases-schema-after-installing-sql-server-update.md)  
  
  
