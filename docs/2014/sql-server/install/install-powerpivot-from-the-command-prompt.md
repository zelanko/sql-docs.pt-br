---
title: Instalar o PowerPivot no prompt de comando | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4677413e517812bf18bc41f59374367b6e27276a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890177"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>Instalar o PowerPivot pelo prompt de comando
  É possível executar a Instalação na linha de comando para instalar o SQL Server PowerPivot para SharePoint. Você deve incluir o parâmetro `/ROLE` no comando e excluir o parâmetro `/FEATURES`.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 O SharePoint Server 2010 Enterprise Edition com Service Pack 1 (SP1) deve ser instalado.  
  
 Você deve usar contas de domínio para provisionar o Analysis Services.  
  
 O computador deve ingressar no mesmo domínio do farm do SharePoint.  
  
##  <a name="Commands"></a>Opções de instalação baseadas em/ROLE  
 Para implantações do PowerPivot para SharePoint, o parâmetro `/ROLE` é usado no lugar do parâmetro `/FEATURES`. Os valores válidos incluem:  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 Ambas as funções instalam arquivos de aplicativo, de configuração e de implantação que permitem a execução de um PowerPivot para SharePoint em um farm do SharePoint. A especificação de uma função fará a Instalação verificar os requisitos de hardware e de software necessários à integração com o SharePoint.  
  
 A opção de farm existente pressupõe que um farm do SharePoint já está em vigor. A nova opção de farm pressupõe que você criará um novo farm; Ele dá suporte à adição de uma instância de Mecanismo de Banco de Dados na sintaxe de linha de comando para que você possa usar a instância de Mecanismo de Banco de Dados como o servidor de banco de dados do farm.  
  
 Em comparação com as versões anteriores, todas as tarefas de configuração de servidor são executadas como tarefas pós-instalação. Se você estiver automatizando as etapas de instalação e configuração, poderá usar o PowerShell para configurar o servidor. Para obter mais informações, consulte [configuração do PowerPivot usando o Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell).  
  
## <a name="example-commands"></a>Comandos de exemplo  
 Os exemplos a seguir ilustram o uso de cada opção. O exemplo 1 `SPI_AS_ExistingFarm`mostra.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 O Exemplo 2 mostra `SPI_AS_NewFarm`. Observe que isso inclui parâmetros para o provisionamento do Mecanismo de Banco de Dados.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="Join"></a>Modificando a sintaxe do comando  
 Use as etapas a seguir para modificar a sintaxe do comando de exemplo.  
  
1.  Copie e cole o seguinte comando no Bloco de Notas:  
  
    ```  
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     O parâmetro `/q` executa a Instalação no modo silencioso, que suprime a interface do usuário.  
  
     O `/IAcceptSQLServerLicenseTerms` será obrigatório quando o parâmetro `/q` ou `/qs` for especificado para instalações autônomas.  
  
     O parâmetro `/action` instrui a Instalação a executar uma instalação.  
  
     O parâmetro `/role` instrui a Instalação a instalar o programa Analysis Services e os arquivos de configuração necessários para o PowerPivot para SharePoint. Essa função também detecta e usa as informações de conectividade do farm existente para acessar o banco de dados de configuração do SharePoint. Este parâmetro é obrigatório. Use-o em lugar do parâmetro `/features` para especificar os componentes a serem instalados.  
  
     O parâmetro `/instancename` especifica 'PowerPivot' como uma instância nomeada. Esse valor é embutido em código e não pode ser alterado. Ele está especificado no comando para fins instrutivos para que você saiba como o serviço é instalado.  
  
     O parâmetro `/indicateprogress` permite monitorar o andamento na janela do prompt de comando.  
  
2.  O parâmetro `PID` é omitido do comando, o que faz a edição Evaluation ser instalada. Se você quiser instalar a edição Enterprise, adicione o PID ao comando da Instalação e forneça uma chave de produto válida.  
  
    ```  
  
    /PID=<product key for an Enterprise installation>  
  
    ```  
  
3.  Substitua os espaços reservados para \<o domínio \ \<nomedousuário > e senha forte > com contas de usuário e senhas válidas.  
  
     Os `/assvaccount` parâmetros e **/assvcpassword** são usados para configurar a [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] instância no servidor de aplicativos. Substitua esses espaços reservados pelas informações de conta válidas.  
  
     O parâmetro **/assysadminaccounts** deve ser definido como a identidade do usuário que está executando SQL Server configuração. Você deve especificar pelo menos um administrador de sistema. Observe que a Instalação do SQL Server deixou de conceder permissões sysadmin para membros do grupo Administradores interno.  
  
4.  Remova quebras de linha.  
  
5.  Selecione o comando inteiro e, em seguida, clique em **copiar** no menu Editar.  
  
6.  Abra um prompt de comando do administrador. Para fazer isso, clique em **Iniciar**, clique com o botão direito do mouse no prompt de comando e selecione **Executar como administrador**.  
  
7.  Navegue para a unidade ou pasta compartilhada que contém a mídia de instalação do SQL Server.  
  
8.  Cole o comando revisado na linha de comando. Para fazer isso, clique no ícone no canto superior esquerdo da janela do prompt de comando, aponte para **Editar**e clique em **colar**.  
  
9. Pressione **Enter** para executar o comando. Aguarde a conclusão da instalação. É possível monitorar o andamento da Instalação na janela do prompt de comando.  
  
10. Para verificar a instalação, consulte o arquivo summary.txt em \Arquivos de Programas\SQL Server\120\Setup Bootstrap\Log. O resultado final deverá indicar "Aprovado" se o servidor for instalado sem erros.  
  
11. Configure o servidor. Você deve, no mínimo, implantar soluções, criar um aplicativo de serviço e habilitar o recurso de cada conjunto de sites. Para obter mais informações, consulte [Configurar ou reparar a &#40;&#41; ferramenta de configuração do PowerPivot PowerPivot para SharePoint 2010](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md) ou a [Administração e a configuração do servidor PowerPivot na administração central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
