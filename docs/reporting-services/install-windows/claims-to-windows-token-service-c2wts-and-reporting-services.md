---
title: Claims to Windows Token Service (c2WTS) e do Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: c0190e9e7a7194f6d848b56a72953f81a0002f98
ms.contentlocale: pt-br
ms.lasthandoff: 08/17/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>C2WTS (Declarações para Serviço de Token do Windows) e Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  O C2WTS (Declarações para Serviço de Token do Windows) do SharePoint será necessário com o modo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SharePoint se você desejar usar a autenticação do Windows para fontes de dados que estejam fora do farm do SharePoint. Isso ocorre mesmo quando o usuário acessa as fontes de dados com a Autenticação do Windows porque a comunicação entre o WFE (front-end da Web) e o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sempre será uma Autenticação de Declarações.  
  
 O c2WTS é necessário até mesmo quando as fontes de dados estão no mesmo computador que o serviço compartilhado. Entretanto, neste cenário, a delegação restrita não é necessária.  
  
 Os tokens criados por c2WTS só funcionarão com a delegação restrita (restrições a serviços específicos) e a opção de configuração "usando qualquer protocolo de autenticação". Conforme observado anteriormente, se suas fontes de dados estiverem no mesmo computador que o serviço compartilhado, a delegação restrita não será necessária.  
  
 Se seu ambiente usar a delegação restrita de Kerberos, o serviço do SharePoint Server e as fontes de dados externas precisarão residir no mesmo domínio do Windows. Qualquer serviço que dependa do c2WTS (Declarações para Serviço de Token do Windows) deve usar a delegação **restrita** Kerberos para permitir que o c2WTS use a transição do protocolo Kerberos para traduzir declarações em credenciais do Windows. Estes requisitos são verdadeiros para todos os Serviços Compartilhados do SharePoint. Para obter mais informações, consulte [Plano para autenticação Kerberos no SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  
  
 O procedimento é resumido neste tópico.

## <a name="prerequisites"></a>Pré-requisitos

> [!NOTE]
>  Nota: Algumas das etapas de configuração podem mudar ou não funcionar em certas topologias de farm. Por exemplo, uma única instalação de servidor não oferece suporte aos serviços Windows Identity Foundation c2WTS; portanto, cenários de delegação de declarações para token do windows não são possíveis com esta configuração de farm.

> [!IMPORTANT]
> Se estiver usando o Power View para trabalhar em pastas de trabalho Power Pivot, você precisará definir configurações adicionais para [Visão geral do Office Server Online](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx). Para obter mais informações, consulte os white papers a seguir. 
>
> - [Implantação do SQL Server 2016 PowerPivot e Power View no SharePoint 2016](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
> 
> - [Implantando o SQL Server 2016 PowerPivot e Power View em um farm multicamadas do SharePoint 2016](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>Etapas básicas necessárias para configurar o c2WTS  
  
1.  Configure a conta de serviço do c2WTS. Adicione a conta de serviço ao grupo de Administradores local em cada servidor de aplicativos executando c2WTS. Além disso, verifique se a conta tem os seguintes direitos de política de segurança local:  
  
    -   Atuar como parte do sistema operacional  
  
    -   Representar um cliente após a autenticação  
  
    -   Fazer logon como um serviço  
  
2.  Configure a delegação para a conta de serviço c2WTS. A conta precisa de Delegação Restrita com Transição de Protocolo e de permissões para delegar aos Serviços com os quais ela precisa se comunicar (isto é, SQL Server Engine, SQL Server Analysis Services). Para configurar a delegação, você pode usar o snap-in Usuários e Computador do Active Directory.  

    > [!IMPORTANT]
    > Todas as configurações que você definir para a conta de serviço C2WTS na guia delegação precisarão corresponder à conta de serviço do Reporting Services. Por exemplo, se você permitir que a conta de serviço do C2WTS delegue para um Serviço SQL, será necessário fazer o mesmo na conta de serviço do Reporting Services.
  
    1.  Clique com o botão direito do mouse em cada conta de serviço e abra a caixa de diálogo de propriedades. Na caixa de diálogo, clique na guia **Delegação** .  
  
        > [!NOTE]  
        >  Observação: a guia delegação só ficará visível se o objeto tiver um SPN (Nome da Entidade de Serviço) atribuído a ele. c2WTS does not require an SPN on the c2WTS Account, however, without an SPN, the **Delegação** não ficará visível. Um modo alternativo de configurar a delegação restrita é usar um utilitário como **ADSIEdit**.  
  
    2.  Principais opções de configuração na guia delegação:  
  
        -   Selecione "Confiar neste usuário apenas para delegação a serviços especificados"  
  
        -   Selecione "Usar qualquer protocolo de autenticação"  

    3. Selecione **Adicionar** para adicionar um serviço para delegação.
    
    4. Selecione **usuários ou computadores...** * e insira a conta que hospeda o serviço. Por exemplo, se um SQL Server está em execução em uma conta denominada *sqlservice*, digite `sqlservice`.
    
    5. Selecione a lista de serviços. Isso mostrará os SPNs que estão disponíveis nessa conta. Se você não vir o serviço listado nessa conta, ele pode estar ausente ou colocado em uma conta diferente. Você pode usar o utilitário SetSPN para ajustar os SPNs.
    
    6. Selecione OK para sair das caixas de diálogo.
  
3.  Configure o c2WTS ‘AllowedCallers’  
  
     O c2WTS requer as identidades dos “chamadores” explicitamente listadas no arquivo de configuração, **c2wtshost.exe.config**. O c2WTS não aceita solicitações de todos os usuários autenticados no sistema, a menos que esteja configurado para fazer desse modo. Neste caso, o 'chamador' é o grupo WSS_WPG do Windows. O arquivo c2wtshost.exe.confi é salvo no seguinte local:  
     
     > [!NOTE]
     > Alterar a conta de serviço na Administração Central do SharePoint para o serviço C2WTS adicionará essa conta ao grupo WSS_WPG.
  
     **\Arquivos de Programas\Windows Identity Foundation\v3.5\c2WTShost.exe.config**  
  
     Este é um exemplo do arquivo de configuração:  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```    
4.  Inicie o “Claims to Windows Token Service” do SharePoint: Inicie o Claims to Windows Token Service pela Administração Central do SharePoint na página **Gerenciar serviços no servidor** . O serviço deverá ser iniciado no servidor que estará executando a ação. Por exemplo, se você tiver um servidor que é um WFE e outro servidor que é um Servidor de aplicativos com o serviço compartilhado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] shared service running, you only need to start c2WTS on the Application Server. O c2WTS não é necessário no WFE.

## <a name="next-steps"></a>Próximas etapas

[Visão geral de reivindicações do Windows Token Service (c2WTS)](http://msdn.microsoft.com/library/ee517278.aspx)   
[Plano para autenticação Kerberos no SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
