---
title: "Configurações de email – modo nativo do Reporting Services (Gerenciador de Configurações) | Microsoft Docs"
ms.custom: 
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: SQL13.rsconfigtool.emailsettings.F1
helpviewer_keywords: SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 4f4a978424825e4f54596ec2485818b47ce4d0c9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="e-mail-settings---reporting-services-native-mode-configuration-manager"></a>Configurações de email - Modo Nativo do Reporting Services (Gerenciador de Configurações)
O Reporting Services inclui uma extensão de entrega de email, para que você possa distribuir relatórios por email. Dependendo de como você definir a assinatura de email, uma entrega pode consistir em uma notificação, um link, um anexo ou um relatório inserido. A extensão de entrega de email funciona com sua tecnologia de servidor de email existente. O servidor de email deve ser um encaminhador ou servidor SMTP. O servidor de relatório se conecta a um servidor SMTP por meio de bibliotecas (cdosys.dll) de CDO (Collaboration Data Objects) que são fornecidas pelo sistema operacional.

A extensão de entrega de email do servidor de relatório não é configurada por padrão. Você deve usar o Gerenciador de Configurações do Reporting Services para configurar a extensão de forma mínima. Para definir propriedades avançadas, você deve editar o arquivo RSReportServer.config. Se não for possível configurar o servidor de relatório para usar essa extensão, em vez disso você poderá entregar relatórios para uma pasta compartilhada. Para obter mais informações, veja Entrega de arquivo compartilhado no Reporting Services.

## <a name="configuration-requirements"></a>Requisitos de configuração

- A entrega de email do servidor de relatório é implementada em CDO (Collaboration Data Objects) e requer um servidor SMTP local ou remoto ou um encaminhador SMTP. Não há suporte ao SMTP em todos os sistemas operacionais Windows. Se você estiver usando a edição com base em Itanium do Windows Server 2008, não haverá suporte ao SMTP. Para obter mais informações sobre as opções de configuração fornecidas por CDO, consulte [Configuration CoClass](http://go.microsoft.com/fwlink/?LinkId=98237) (em inglês) no MSDN.

A conta de autenticação configurada deve ter permissão no servidor SMTP para enviar email.

- A extensão de entrega de email usa a codificação UTF-8 em anexos de email. Você não pode modificar a codificação; a extensão de renderização HTML só dá suporte a UTF-8.

> [!NOTE] 
> A extensão de entrega de email padrão não dá suporte para assinar digitalmente ou criptografar mensagens de email de saída.

## <a name="setting-configuration-options-for-e-mail-delivery"></a>Definindo opções de configuração para entrega de email
Antes de usar a entrega de email do Servidor de Relatório, você deve definir valores de configuração que forneçam informações sobre qual servidor SMTP será usado.

Para configurar um servidor de relatório para entrega de email, faça o seguinte:

- Use o Gerenciador de Configurações do Reporting Services se estiver especificando somente um servidor SMTP e uma conta de usuário que tenha permissão para enviar email. Essas são as configurações mínimas necessárias para a configuração da extensão de entrega de email do Servidor de Relatório.

- (Opcionalmente) Use um editor de texto para especificar configurações adicionais no arquivo RSreportserver.config. Esse arquivo contém todos os parâmetros de configuração para a entrega de email do Servidor de Relatório. Será necessário especificar configurações adicionais nesses arquivos se você estiver usando um servidor SMTP local ou se estiver restringindo a entrega de email para hosts específicos. Para obter mais informações sobre como encontrar e modificar arquivos de configuração, veja [Modificar um arquivo de configuração do Reporting Services (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) nos Manuais Online do SQL Server.

> [!NOTE] 
> As configurações de email do servidor de relatório têm como base o CDO. Para obter mais detalhes sobre configurações específicas, você pode consultar a documentação de produção do CDO.

## <a name="a-namersconfigmanconfigure-report-server-e-mail-using-the-reporting-services-configuration-manager"></a><a name="rsconfigman"/>Configurar o email do servidor de relatório usando o Reporting Services Configuration Manager

1. Inicie o Gerenciador de Configurações do Reporting Services e conecte-se à instância do servidor de relatório.

2. Em **Endereço do Remetente**, insira o endereço de email a ser usado no campo **De:** de um email gerado. 

     Você deve especificar uma conta de usuário que tenha permissão para enviar email do servidor SMTP. O valor digitado para o **Endereço do Remetente** é salvo no campo `<From>` do arquivo rsreportserver.config.  

3.  Em **Servidor SMTP**, especifique o servidor SMTP ou o gateway a ser usado. 

     Esse valor pode ser um endereço IP, um nome NetBIOS de um computador em sua intranet corporativa ou um nome de domínio totalmente qualificado. O valor digitado para o **Servidor SMTP** é salvo no campo `<SMTPServer>` do arquivo rsreportserver.config.

4. Use a lista suspensa **Autenticação** para especificar a autenticação para o servidor SMTP. Esse 

     - **Nenhuma autenticação** significa que você se conectará de forma anônima ao servidor de email especificado.
     
          A seleção desta opção definirá `<SendUsing>` com o valor de **2** e `<SMTPAuthenticate>` com um valor de **0** em rsreportserver.config.
     
     - **Nome de usuário e senha (Básico)** permite especificar um nome de usuário e uma senha para se conectar ao servidor de email. Também é possível selecionar **Usar conexão segura** para que isso passe por uma conexão criptografada ao servidor de email.
     
          A seleção desta opção definirá `<SendUsing>` com o valor de **2** e `<SMTPAuthenticate>` com um valor de **1** em rsreportserver.config. A seleção de **Usar conexão segura** definirá `SMTPUseSSL` como **True**. **Nome de usuário** será definido em `<SendUserName>` como um valor criptografado. **Senha** será definida em `<SendPassword>` como um valor criptografado.
     
     - **Conta de serviço do servidor de relatório (NTLM)** usará a conta de serviço especificada para o servidor de relatório. Se você estiver usando a conta de serviço do servidor de relatório para autenticação, verifique se a conta de serviço tem as permissões **Send As** no servidor SMTP.
     
          A seleção desta opção definirá `<SendUsing>` com o valor de **2** e `<SMTPAuthenticate>` com um valor de **2** em rsreportserver.config.

5. Escolha **Aplicar**.

6. Opcionalmente, você pode ajustar os campos adicionais, para a configuração de email, em rsreportserver.config.

## <a name="example-report-server-e-mail-configuration"></a>Exemplo de configuração de email do servidor de relatório
O exemplo a seguir ilustra as configurações no arquivo RSreportserver.config para um servidor SMTP remoto. Para ler sobre as descrições da configuração e os valores válidos, veja [Arquivo de configuração rsreportserver.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) nos Manuais Online do SQL Server.

```
<RSEmailDPConfiguration>
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>
     <SMTPServerPort></SMTPServerPort>
     <SMTPAccountName></SMTPAccountName>
     <SMTPConnectionTimeout></SMTPConnectionTimeout>
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>
     <SMTPUseSSL>False</SMTPUseSSL>
     <SendUsing>2</SendUsing>
     <SMTPAuthenticate>2</SMTPAuthenticate>
     <From>my-rs-email-account@Adventure-Works.com</From>
     <EmbeddedRenderFormats>
          <RenderingExtension>MHTML</RenderingExtension>
     </EmbeddedRenderFormats>
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>
     <ExcludedRenderFormats>
          <RenderingExtension>HTMLOWC</RenderingExtension>
          <RenderingExtension>NULL</RenderingExtension>
          <RenderingExtension>RGDI</RenderingExtension>
     </ExcludedRenderFormats>
     <SendEmailToUserAlias>True</SendEmailToUserAlias>
     <DefaultHostName></DefaultHostName>
     <PermittedHosts>
          <HostName>Adventure-Works.com</HostName>
          <HostName>hotmail.com</HostName>
     </PermittedHosts>
     <SendUserName></SendUserName>
     <SendPassword></SendPassword>
</RSEmailDPConfiguration>
```
## <a name="configuration-options-for-setting-the-to-field-in-a-message"></a>Opções de configuração para a definição do campo Para: em uma mensagem
As assinaturas definidas pelo usuário que forem criadas de acordo com as permissões concedidas pela tarefa Gerenciar assinaturas individuais contêm um nome de usuário predefinido que tem como base a conta de usuário do domínio. Quando o usuário cria a assinatura, o nome do destinatário no campo **Para:** é endereçado a si mesmo, usando a conta do usuário do domínio da pessoa que está criando a assinatura.

Se você estiver usando um servidor ou encaminhador SMTP que use contas de email diferentes da conta de usuário do domínio, a entrega do relatório falhará quando o servidor SMTP tentar entregar o relatório para esse usuário.

Para solucionar esse erro, você pode modificar os parâmetros de configuração que permitem aos usuários inserir um nome no campo **Para:** :

1. Abra RSReportServer.config com um editor de texto.

2. Defina `<SendEmailToUserAlias>` como **False**.

3. Defina `<DefaultHostName>` como o nome DNS (Sistema de Nome de Domínio) ou o endereço IP do servidor ou encaminhador SMTP.

4. Salve o arquivo.

## <a name="configuration-options-for-remote-smtp-service"></a>Opções de configuração para o serviço SMTP remoto
A conexão entre o servidor de relatório e um encaminhador ou servidor SMTP é determinada pelos seguintes parâmetros de configuração:

- `<SendUsing>` especifica um método para o envio de mensagens. Você pode escolher entre um serviço de rede SMTP ou um diretório local de retirada de serviço SMTP. Para usar um serviço SMTP remoto, este valor deve ser definido como **2** no arquivo RSReportServer.config.
- `<SMTPServer>` especifica o encaminhador ou servidor SMTP remoto. Esse valor será necessário se você estiver usando um encaminhador ou servidor SMTP remoto.
- `<From>` define o valor que aparece na linha **De:** de uma mensagem de email. Esse valor será necessário se você estiver usando um encaminhador ou servidor SMTP remoto.

Outros valores usados para o serviço SMTP remoto incluem os seguintes (observe que não é necessário especificar esses valores, a menos que deseje substituir os valores padrão).

- `<SMTPServerPort>` está configurado para a porta 25 por padrão.
- `<SMTPAuthenticate>` especifica como o servidor de relatório se conecta ao servidor SMTP remoto. O valor padrão é **0** (sem autenticação). Nesse caso, a conexão é feita por acesso Anônimo. Dependendo da configuração do domínio, o servidor de relatório e o servidor SMTP podem precisar ser membros do mesmo domínio.
- Para enviar email para listas de distribuição restritas (por exemplo, listas de distribuição que aceitem mensagens de entrada apenas de contas autenticadas), defina `<SMTPAuthenticate>` como **1** ou **2**. Se você defini-lo como **1**, também será necessário definir `<SendUserName>` e `<SendPassword>`. É recomendável fazer isso por meio do Reporting Services Configuration Manager, já que ele criptografa os valores para `<SendUserName>` e `<SendPassword>`.

### <a name="to-configure-a-remote-smtp-service-for-the-report-server"></a>Para configurar um serviço SMTP remoto para o servidor de relatório

> [!NOTE] 
> É recomendável configurar o servidor de email por meio do Reporting Services Configuration Manager.

1. Verifique se o serviço do Windows Servidor de Relatório tem permissões **Send As** no servidor SMTP.

2. Abra o arquivo RSReportServer.config em um editor de texto.

3. Verifique se `<UrlRoot>` está configurado como o endereço da URL do servidor de relatório. Esse valor é definido quando você configura o servidor de relatório e já deveria estar preenchido. Se não estiver definido, digite o endereço da URL do servidor de relatório.

4. Na seção Entrega, localize `<RSEmailDPConfiguration>`.
     
5. Em `<SMTPServer>`, digite o nome do servidor SMTP. Esse valor pode ser um endereço IP, um nome UNC de um computador em sua intranet corporativa ou um nome de domínio totalmente qualificado.

6. Defina `<SendUsing>` com um valor de **2** para usar a conta de serviço do servidor de relatório. Defina `<SendUsing>` com um valor de **1** para autenticação básica. Se você defini-lo como **1**, você também precisará fornecer um valor para `<SendUserName>` e `<SendPassword>`. Se você quiser que esses valores sejam criptografados, defina a autenticação no Reporting Services Configuration Manager.

7. Defina `<SMTPAuthenticate>` com um valor de **1** se você definir `<SendUsing>` como 1 ou 2.

7. Defina `<From>`. Você deve especificar uma conta de usuário que tenha permissão para enviar email do servidor SMTP.

8. Salve o arquivo.

     O servidor de relatório usará as novas configurações automaticamente; você não precisa reiniciar o serviço. Você pode especificar configurações adicionais de SMTP para configurar mais como o servidor SMTP é usado para entrega de email do servidor de relatório.

## <a name="configuration-options-for-local-smtp-service"></a>Opções de configuração para o serviço SMTP local
A configuração de um serviço SMTP local será útil se você estiver testando ou solucionando problemas de entrega de email do servidor de relatório. O serviço SMTP local não está habilitado por padrão.

A conexão entre o servidor de relatório e um encaminhador ou servidor SMTP local é determinada pelos seguintes parâmetros de configuração:

- **SendUsing** é definido como **1**.
- **SMTPServerPickupDirectory** é definido como uma pasta na unidade local.

  > [!NOTE] 
  > Lembre-se de não definir SMTPServer se estiver usando um servidor SMTP local.

- **De** define o valor que aparece na linha **De:** de uma mensagem de email. Esse valor é necessário.

### <a name="to-configure-a-local-smtp-service-for-the-report-server"></a>Para configurar um serviço SMTP local para o servidor de relatório

1. No Painel de Controle, selecione **Ativar ou desativar recursos do Windows** para iniciar o **Assistente para Adicionar Funções e Recursos**.

2. Selecione **Instalação baseada em função ou recurso** e selecione **Avançar**.

3. Selecione o servidor no qual será instalado o IIS (Servidor de Informações da Internet) e selecione **Avançar**.

4. Selecione **Avançar** na página *Funções de Servidor**.
     
5. Na página *Recursos* , selecione **Servidor SMTP** e **Avançar**.

     Se for solicitado que você adicione recursos necessários ao Servidor SMTP, selecione **Adicionar Recursos**.

6. Selecione **Avançar** na página *Função de Servidor Web (IIS)* .

7. Selecione **Avançar** na página *Serviços de Função* .

8. Selecione **Instalar** na página **Confirmação** .

9. Verifique se o serviço Windows **Protocolo SMTP** está em execução no console de Serviços.

     Para configurar o servidor SMTP local, você precisará usar o Gerenciador do IIS 6.0 em Ferramentas administrativas.

10. Abra o arquivo RSReportServer.config em um editor de texto.

11. Verifique se `<UrlRoot>` está configurado como o endereço da URL do servidor de relatório. Esse valor é definido quando você configura o servidor de relatório e já deveria estar preenchido. Se ele não for definido, digite a URL do serviço Web do servidor de relatório.

12. Na seção Entrega, localize `<RSEmailDPConfiguration>`.
     
13. Verifique se `<SMTPServer>` está presente, mas vazio.
     
14. Defina `<SendUsing>` como 1.
     
14. Defina `<SMTPAuthenticate>` como 0.
     
15. Defina `<SMTPServerPickupDirectory>` como a pasta de Retirada de Serviço SMTP.
     
     O local padrão será *C:\inetpub\mailroot\Pickup*.
     
16. Defina `<From>`. Isto define o valor que aparece na linha **De:** de uma mensagem de email.
     
17. Salve o arquivo.
  
## <a name="see-also"></a>Consulte também  
[Gerenciador de Configurações do Reporting Services (Modo Nativo).](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
[Modify a Reporting Services Configuration File (rsreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
[Arquivo de configuração rsreportserver.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)
  
  
