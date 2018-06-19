---
title: Gerenciar certificados do SQL Server Integration Services Scale Out | Microsoft Docs
ms.description: This article describes how to manage certificates to secure communications between SSIS Scale Out Master and Scale Out Workers.
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.custom: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: e602b89a44b5d26369973ef6f5ec8dc1f6d5c4eb
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35405128"
---
# <a name="manage-certificates-for-sql-server-integration-services-scale-out"></a>Gerenciar certificados do SQL Server Integration Services Scale Out

Para proteger a comunicação entre o Mestre do Scale Out e os Trabalhos do Scale Out, o SSIS Scale Out usa dois certificados – um para o Mestre e outro para os Trabalhos. 

## <a name="scale-out-master-certificate"></a>Certificado do Mestre do Scale Out

Na maioria dos casos, o certificado do Mestre do Scale Out é configurado durante a instalação do Mestre do Scale Out.

Na página **Configuração do Integration Services Scale Out – Nó Mestre** do Assistente de Instalação do SQL Server, você pode optar por criar um novo certificado SSL autoassinado ou usar um certificado SSL existente.

![Configuração do Mestre](media/master-config.PNG)

**Novo certificado**. Caso não tenha requisitos especiais de certificados, você poderá optar por criar um novo certificado SSL autoassinado. Você pode ainda especificar os CNs nesse certificado. Verifique se o nome do host do ponto de extremidade mestre a ser usado posteriormente pelo Trabalho do Scale Out está incluído nos CNs. Por padrão, o nome do computador e o endereço IP do nó mestre estão incluídos. 

**Certificado existente**. Se você optar por usar um certificado existente, clique em **Procurar** para selecionar um certificado SSL no repositório de certificados **Raiz** do computador local.

### <a name="change-the-scale-out-master-certificate"></a>Alterar o certificado do Mestre do Scale Out

Talvez você deseje alterar o certificado do Mestre do Scale Out devido à expiração do certificado ou por outros motivos. Para alterar o certificado do Mestre do Scale Out, siga estas etapas:

#### <a name="1-create-an-ssl-certificate"></a>1. Criar um certificado SSL.
Crie e instale um novo certificado SSL no nó Mestre com o seguinte comando:

```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Por exemplo:

```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-the-master-port"></a>2. Associar o certificado à porta do Mestre
Verifique a associação original com o seguinte comando:

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Por exemplo:

```dos
netsh http show sslcert ipport=0.0.0.0:8391
```

Excluir a associação original e configurar a nova associação com os seguintes comandos:

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```

Por exemplo:

```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```

#### <a name="3-update-the-scale-out-master-service-configuration-file"></a>3. Atualizar o arquivo de configuração de serviço do Mestre do Scale Out
Atualize o arquivo de configuração de serviço do Mestre do Scale Out, `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`, no nó Mestre. Atualize **SSLCertThumbprint** para a impressão digital do novo certificado SSL.

#### <a name="4-restart-the-scale-out-master-service"></a>4. Reiniciar o serviço Mestre do Scale Out

#### <a name="5-reconnect-scale-out-workers-to-scale-out-master"></a>5. Reconectar os Trabalhos do Scale Out ao Mestre do Scale Out
Para cada Trabalho do Scale Out, exclua o Trabalho e, em seguida, adicione-o novamente com o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md) ou faça o seguinte:

A.  Instale o certificado SSL do cliente no repositório Raiz do computador local no nó de Trabalho.

B.  Atualize o arquivo de configuração de serviço do Trabalho do Scale Out.

    Update the Scale Out Worker service configuration file, `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`, on the Worker node. Update **MasterHttpsCertThumbprint** to the thumbprint of the new SSL certificate.

c.  Reinicie o serviço Trabalho do Scale Out.

## <a name="scale-out-worker-certificate"></a>Certificado de Trabalho do Scale Out

Durante a instalação do Trabalho do Scale Out, o respectivo certificado é gerado automaticamente. 

### <a name="change-the-scale-out-worker-certificate"></a>Alterar o certificado do Trabalho do Scale Out

Caso deseje alterar o certificado do Trabalho do Scale Out, siga estas etapas:

#### <a name="1-create-a-certificate"></a>1. Criar um certificado
Crie e instale um certificado com o seguinte comando:

```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

Por exemplo:

```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

#### <a name="2-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-worker-node"></a>2. Instalar o certificado do cliente no repositório Raiz do computador local no nó de Trabalho

#### <a name="3-grant-service-access-to-the-certificate"></a>3. Conceder acesso ao certificado para o serviço
Exclua o certificado antigo e conceda acesso ao novo certificado para o serviço do Trabalho do Scale Out com o seguinte comando:

```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```

Por exemplo:

```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```

#### <a name="4-update-the-scale-out-worker-service-configuration-file"></a>4. Atualizar o arquivo de configuração de serviço do Trabalho do Scale Out
Atualize o arquivo de configuração de serviço do Trabalho do Scale Out, `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`, no nó de Trabalho. Atualize **WorkerHttpsCertThumbprint** para a impressão digital do novo certificado.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-master-node"></a>5. Instalar o certificado do cliente no repositório raiz do computador local no nó mestre

#### <a name="6-restart-the-scale-out-worker-service"></a>6. Reiniciar o serviço Trabalho do Scale Out

## <a name="next-steps"></a>Próximas etapas
Para saber mais, veja os tópicos a seguir:
-   [Mestre do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-master.md)
-   [Trabalho do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-worker.md)