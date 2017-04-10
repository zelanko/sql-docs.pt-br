---
title: "Instala&#231;&#245;es Aut&#244;nomas dos Servi&#231;os do SQL Server R | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 14
---
# Instala&#231;&#245;es Aut&#244;nomas dos Servi&#231;os do SQL Server R
    
Antes de iniciar o processo de instalação, Observe estes requisitos:

+ Você deve instalar o mecanismo de banco de dados em cada instância onde você usará os serviços de R (no banco de dados) em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
+ Se você estiver executando uma instalação offline, você deve baixar os componentes necessários do R com antecedência e copiá-los para uma pasta local. Para locais de download, consulte [Instalando componentes R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).   
+ Há um novo parâmetro, */IACCEPTROPENLICENSETERMS*, que indica que você aceitou os termos de licença para usar os componentes de software livre R. Se você não incluir esse parâmetro na linha de comando, a instalação falhará.  
  
## Executar uma Instalação Autônoma dos Serviços do R (No Banco de Dados)  
 O exemplo a seguir mostra os recursos mínimos necessários a serem especificados na linha de comando ao executar uma instalação silenciosa e autônoma dos Serviços do R no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
###  <a name="bkmk_Unattended"></a>  
  
1.  Execute o seguinte comando em um prompt de comando elevado:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
  
2.  Após a conclusão da instalação, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute o comando a seguir para habilitar o recurso.  
  
    ```  
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with  override  
  
    ```  
  
    > [!NOTE]  
    >  Você deve habilitar explicitamente o recurso de mecanismo; caso contrário, não será possível chamar scripts R, mesmo que o recurso tenha sido instalado e configurado pela instalação.  
  
3.  Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso reiniciará automaticamente o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] relacionado também.  
  
## Consulte também  
 [Configuração de Solução de Problemas de R Services](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  