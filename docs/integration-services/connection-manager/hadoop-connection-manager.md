---
title: "Gerenciador de Conexões do Hadoop – SQL Server Integration Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a86643971e12007cd14d902a63ac4bbcd30ba685
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="hadoop-connection-manager"></a>Gerenciador de conexões do Hadoop
  O Gerenciador de Conexões do Hadoop permite que um pacote do SSIS (SQL Server Integration Services) se conecte a um cluster Hadoop usando os valores especificados para as propriedades.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Configurar o Gerenciador de Conexões do Hadoop  
  
1.  Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS**, escolha **Hadoop** > **Adicionar**. A caixa de diálogo **Gerenciador de conexões do Hadoop** se abre.  
  
2.  Para configurar as informações do cluster Hadoop, escolha a guia **WebHCat** ou **WebHDFS** no painel esquerdo.
  
3.  Se você habilitar a opção **WebHCat** para invocar um trabalho de Hive ou Pig no Hadoop, faça o seguinte: 
  
    1.  Para o **Host WebHCat**, insira o servidor que hospeda o serviço WebHCat.  
  
    2.  Para a **Porta WebHCat**, insira a porta do serviço WebHCat, que é 50111 por padrão.  
  
    3.  Escolha o método de **Autenticação** para acessar o serviço WebHCat. Os valores disponíveis são **Básico** e **Kerberos**.  
  
         ![Captura de tela do Editor de Gerenciador de Conexões do Hadoop com a autenticação básica](../../integration-services/connection-manager/media/hadoop-cm-basic.png "Editor de gerenciador de conexões do Hadoop com a autenticação básica")  
  
         ![Captura de tela do Editor de Gerenciador de Conexões do Hadoop com a autenticação Kerberos](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Editor de gerenciador de conexões do Hadoop com a autenticação Kerberos")  
  
    4.  Para o **Usuário WebHCat**, insira o **Usuário** autorizado a acessar o WebHCat.  
  
    5.  Se você escolher a autenticação **Kerberos** , insira a **Senha** e o **Domínio**do usuário.  
  
4.  Se você habilitar a opção **WebHDFS** para copiar dados de ou para o HDFS, faça o seguinte: 
  
    1.  Para o **Hóspede WebHDFS**, insira o servidor que hospeda o serviço WebHDFS.  
  
    2.  Para a **Porta WebHDFS**, insira a porta do serviço WebHDFS, que é 50070 por padrão.  
  
    3.  Selecione o método de **Autenticação** para acessar o serviço WebHDFS. Os valores disponíveis são **Básico** e **Kerberos**.  
  
    4.  Para o **Usuário WebHDFS**, insira o usuário autorizado a acessar o HDFS.  
  
    5.  Se você escolher a autenticação **Kerberos** , insira a **Senha** e o **Domínio**do usuário.  
  
5.  Selecione **Testar Conexão**. (Apenas a conexão que você habilitou é testada.)  
  
6.  Clique em **OK** para fechar a caixa de diálogo.  

## <a name="connect-with-kerberos-authentication"></a>Conecte-se com a autenticação Kerberos
Há duas opções para configurar o ambiente local. Assim, você pode usar a autenticação Kerberos com o Gerenciador de Conexões do Hadoop. Você pode escolher a opção que melhor se ajusta às suas circunstâncias.
-   Opção 1: [ingressar o computador do SSIS ao realm do Kerberos](#kerberos-join-realm)
-   Opção 2: [habilitar a confiança mútua entre o domínio do Windows e o realm do Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Opção 1: ingressar o computador do SSIS ao realm do Kerberos

#### <a name="requirements"></a>Requisitos:

-   O computador do gateway precisa ingressar o realm do Kerberos e não pode ingressar em nenhum domínio do Windows.

#### <a name="how-to-configure"></a>Como configurar:

No computador do SSIS:

1.  Execute o utilitário **Ksetup** para configurar o realm e servidor KDC (Centro de Distribuição de Chaves) do Kerberos.

    O computador deve estar configurado como um membro de um grupo de trabalho, pois o realm do Kerberos é diferente de um domínio do Windows. Defina o realm do Kerberos e adicione um servidor KDC, conforme mostrado no exemplo a seguir. Substitua o `REALM.COM` com seu respectivo realm, conforme necessário.

    ```    
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    Após a execução desses comandos, reinicie o computador.

2.  Verifique a configuração com o comando **Ksetup**. A saída deverá ser semelhante a esta amostra:

    ```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="kerberos-mutual-trust"></a>Opção 2: habilitar a confiança mútua entre o domínio do Windows e o realm do Kerberos

#### <a name="requirements"></a>Requisitos:
-   O computador do gateway deve ingressar em um domínio do Windows.
-   Você precisa de permissão para atualizar as configurações do controlador de domínio.

#### <a name="how-to-configure"></a>Como configurar:

> [!NOTE]
> Substitua o `REALM.COM` e `AD.COM` no tutorial a seguir com seus respectivos realm e controlador de domínio, conforme necessário.

No servidor do KDC:

1.  Edite a configuração do KDC no arquivo **krb5.conf**. Permita que o KDC confie no domínio do Windows, consultando o seguinte modelo de configuração. Por padrão, a configuração está localizada em **/etc/krb5.conf**.

    ```
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    Reinicie o serviço do KDC após a configuração.

2.  Prepare uma entidade de segurança nomeada **krbtgt/REALM.COM@AD.COM** no servidor do KDC. Use o seguinte comando:

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  No arquivo de configuração de serviço do HDFS **hadoop.security.auth_to_local**, adicione `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

No controlador de domínio:

1.  Execute o seguinte comando **Ksetup** para adicionar uma entrada de realm:

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  Estabeleça a confiança do domínio do Windows para o realm do Kerberos. No exemplo a seguir, `[password]` é a senha para a entidade de segurança **krbtgt/REALM.COM@AD.COM**.

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  Selecione um algoritmo de criptografia para ser usado com o Kerberos.

    1. Vá para **Gerenciador do Servidor** > **Gerenciamento de Política de Grupo** > **Domínio**. A partir daí, vá para **Objetos de Política de Grupo** > **Política de Domínio Padrão ou Ativo** > **Editar**.

    2. Na janela pop-up do **Editor de Gerenciamento de Política de Grupo**, vá para **Configuração do Computador** > **Políticas** > **Configurações do Windows**. A partir daí, vá para **Configurações de Segurança** > **Políticas Locais** > **Opções de Segurança**. Configure a **Segurança de rede: configure os tipos de Criptografia permitidos para o Kerberos**.

    3. Selecione o algoritmo de criptografia que deseja usar para se conectar ao KDC. Normalmente, você pode selecionar qualquer uma das opções.

        ![Captura de tela dos tipos de criptografia para o Kerberos](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. Use o comando **Ksetup** para especificar o algoritmo de criptografia a ser usado no realm específico.

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  Para usar a entidade de segurança do Kerberos no domínio do Windows, crie o mapeamento entre a conta de domínio e a entidade de segurança do Kerberos.

    1. Vá para **Ferramentas administrativas** > **Computadores e Usuários do Active Directory**.

    2. Configure os recursos avançados selecionando **Exibição** > **Recursos Avançados**.

    3. Localize a conta para a qual deseja criar mapeamentos, clique com o botão direito do mouse para exibir **Mapeamentos de Nome** e, em seguida, selecione o guia **Nomes Kerberos**.

    4. Adicione uma entidade de segurança do realm.

        ![Captura de tela da caixa de diálogo do Mapeamento de Identidade de Segurança](media/hadoop-connection-manager/map-security-identity.png)

No computador do gateway:

Execute os seguintes comandos **Ksetup** para adicionar uma entrada de realm.

    ```
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

## <a name="see-also"></a>Consulte também  
 [Tarefa do Hive do Hadoop](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Tarefa do Pig do Hadoop](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Tarefas do Sistema de Arquivos Hadoop](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
