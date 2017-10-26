---
title: Claims to Windows Token Service (c2WTS) e do Reporting Services | Microsoft Docs
ms.custom: The Claims to Windows Token Service (C2WTS) is used by SharePoint and needs to be configured for Kerberos constrained delegation to work with SQL Server Reporting Services properly.
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 8a478bba3cde66967594d5ef02f867de5b33edd7
ms.contentlocale: pt-br
ms.lasthandoff: 09/15/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) e Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

O Claims to Windows Token Service (C2WTS) do SharePoint será necessário se você deseja exibir relatórios de modo nativo dentro de [web part do Visualizador de relatórios do SQL Server Reporting Services](../report-server-sharepoint/deploy-report-viewer-web-part.md).

C2WTS também é necessária com o modo do SharePoint do SQL Server Reporting Services se você quiser usar a autenticação do Windows para fontes de dados que estão fora do farm do SharePoint. O C2WTS é necessário até mesmo quando as fontes de dados estão no mesmo computador que o serviço compartilhado. Entretanto, neste cenário, a delegação restrita não é necessária.

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

## <a name="report-viewer-web-part-configuration"></a>Configuração da parte do relatório Visualizador da web

A web part do Visualizador de relatórios pode ser usada para inserir relatórios de modo nativo do SQL Server Reporting Services no seu site do SharePoint. Esta web part está disponível para o SharePoint 2013 e SharePoint 2016. SharePoint 2013 e SharePoint 2016 fazem uso de autenticação de declarações. Por padrão, o SQL Server Reporting Services (modo nativo) usa a autenticação do Windows. Como resultado, o C2WTS precisa ser configurado corretamente para relatórios renderizados corretamente.

## <a name="sharepoint-mode-integaration"></a>Integaration de modo do SharePoint

**Esta seção se aplica somente ao SQL Server 2016 Reporting Services e anteriores.**

O Claims to Windows Token Service (C2WTS) do SharePoint é necessário com o modo do SharePoint do SQL Server Reporting Services se você quiser usar a autenticação do Windows para fontes de dados que estão fora do farm do SharePoint. Isso é verdadeiro mesmo se o usuário acessa as fontes de dados com a autenticação do Windows porque a comunicação entre o front-end da web (WFE) e o serviço compartilhado do Reporting Services sempre será uma autenticação de declarações.

## <a name="steps-needed-to-configure-c2wts"></a>Etapas necessárias para configurar o c2WTS

Os tokens criados por C2WTS só funcionarão com a delegação restrita (restrições a serviços específicos) e a opção de configuração "usando qualquer protocolo de autenticação". Conforme observado anteriormente, se suas fontes de dados estiverem no mesmo computador que o serviço compartilhado, a delegação restrita não será necessária.

Se seu ambiente usar a delegação restrita de Kerberos, o serviço do SharePoint Server e as fontes de dados externas precisarão residir no mesmo domínio do Windows. Qualquer serviço que dependa do c2WTS (Declarações para Serviço de Token do Windows) deve usar a delegação **restrita** Kerberos para permitir que o c2WTS use a transição do protocolo Kerberos para traduzir declarações em credenciais do Windows. Estes requisitos são verdadeiros para todos os Serviços Compartilhados do SharePoint. Para obter mais informações, consulte [Plano para autenticação Kerberos no SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  

1. Configure a conta de serviço C2WTS. Adicione a conta de serviço para o grupo de administradores local em cada servidor que o C2WTS será usado.

    Para o **web part do Visualizador de relatórios**, essa será os servidores Web Front End (WFE). Para **modo integrado do SharePoint**, essa será os servidores de aplicativos em que o serviço Reporting Services está em execução.

2. Configure a delegação para a conta de serviço C2WTS.

    A conta precisa de delegação restrita com transição de protocolo e permissões para delegar aos serviços é necessário para se comunicar com (ou seja, SQL Server Database Engine, SQL Server Analysis Services). Para configurar a delegação, você pode usar o snap-in de usuários do Active Directory e o computador e precisará ser um administrador de domínio.

    > [!IMPORTANT]
    > Quaisquer configurações de você configurar para a conta de serviço C2WTS na guia delegação, precisa corresponder à conta de serviço principal que está sendo usada. Para o **web part do Visualizador de relatórios**, essa será a conta de serviço para o aplicativo web do SharePoint. Para **modo integrado do SharePoint**, isso será a conta de serviço do Reporting Services.
    >
    > Por exemplo, se você permitir que a conta de serviço do C2WTS delegue para um serviço do SQL, você precisa fazer o mesmo na conta de serviço do Reporting Services para o modo integrado do SharePoint.

    * Clique com o botão direito do mouse em cada conta de serviço e abra a caixa de diálogo de propriedades. Na caixa de diálogo, clique na guia **Delegação** .

        A guia delegação só ficará visível se o objeto tem um nome de entidade de serviço (SPN) atribuído a ele. C2WTS não requer um SPN na conta de C2WTS; porém, sem um SPN, o **delegação** não ficará visível. Um modo alternativo de configurar a delegação restrita é usar um utilitário como **ADSIEdit**.

    * Principais opções de configuração na guia delegação:

        * Selecione **confiar neste usuário para delegação apenas a serviços especificados**
        * Selecione **usar qualquer protocolo de autenticação**

    * Selecione **Adicionar** para adicionar um serviço para delegação.

    * Selecione **usuários ou computadores...** * e insira a conta que hospeda o serviço. Por exemplo, se um SQL Server está em execução em uma conta denominada *sqlservice*, digite `sqlservice`. 

    * Selecione a lista de serviços. Isso mostrará os SPNs que estão disponíveis nessa conta. Se você não vir o serviço listado nessa conta, ele pode estar ausente ou colocado em uma conta diferente. Você pode usar o utilitário SetSPN para ajustar os SPNs.

    * Selecione OK para sair das caixas de diálogo.

3. Configurar o C2WTS *AllowedCallers*.

    C2WTS requer as identidades dos 'chamadores' explicitamente listadas no arquivo de configuração, **c2wtshost.exe**. O C2WTS não aceita solicitações de todos os usuários autenticados no sistema, a menos que esteja configurado para fazer assim. Nesse caso o 'chamador' é o grupo do Windows WSS_WPG. O arquivo c2wtshost.exe. Confi é salvo no seguinte local:

    Alterar a conta de serviço na Administração Central do SharePoint para o serviço C2WTS adicionará essa conta ao grupo WSS_WPG.

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

4. Inicie o Claims to Windows Token Service pela Administração Central do SharePoint no **gerenciar serviços no servidor** página. O serviço deverá ser iniciado no servidor que estará executando a ação. Por exemplo, se você tiver um servidor que é um WFE e outro servidor que é um servidor de aplicativos que tem o serviço compartilhado do SQL Server Reporting Services em execução, você só precisam iniciar o C2WTS no servidor de aplicativos. C2WTS só é necessário em um servidor WFE, se você estiver executando a web part do Visualizador de relatórios.

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
