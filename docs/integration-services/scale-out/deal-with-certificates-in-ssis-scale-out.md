---
title: Lidar com certificados no SQL Server Integration Services Scale Out | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e09fec1fcf9cf0221dad50d708adef773b297237
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>Lidar com certificados no SQL Server Integration Services Scale Out

Para proteger a comunicação entre Mestre do Scale Out e Trabalho do Scale Out, dois certificados são usados no Scale Out, ou seja, o certificado do Mestre do Scale Out e o do Trabalho do Scale Out. 

## <a name="scale-out-master-certificate"></a>Certificado do Mestre do Scale Out

Na maioria dos casos, o certificado do Mestre do Scale Out é configurado durante a instalação do Mestre do Scale Out.

Na página **Configuração do Integration Services Scale Out – Nó Mestre** do Assistente de Instalação do SQL Server, você pode optar por criar um novo certificado SSL autoassinado ou usar um certificado SSL existente.

![Configuração do Mestre](media/master-config.PNG)

Se você não tem requisitos especiais de certificados, você pode optar por criar um novo certificado SSL autoassinado. Você pode ainda especificar os CNs nesse certificado. Verifique se o nome do host do ponto de extremidade mestre usado pelo Trabalho do Scale Out posteriormente está incluído nos CNs. Por padrão, o nome do computador e o IP do nó mestre estão incluídos. 

Se você optar por usar um certificado existente, clique em "Procurar..." para selecionar um certificado SSL do repositório de certificados **raiz** do computador local.

### <a name="change-scale-out-master-certificate"></a>Alterar certificado do Mestre do Scale Out

Você talvez queira alterar o certificado do Mestre do Scale Out devido à expiração do certificado ou por outros motivos. Siga as etapas abaixo:

#### <a name="1-create-a-ssl-certificate"></a>1. Criar um certificado SSL.
Criar e instalar um certificado SSL no nó Mestre com o seguinte comando:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Exemplo:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. Associar o certificado à porta do Mestre
Verifique a associação original com o comando:
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
Exemplo:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
Excluir a associação original e configurar a nova associação com os seguintes comandos:
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
Exemplo:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Atualizar o arquivo de configuração de serviço do Mestre de Scale Out
Atualize o arquivo de configuração de serviço Mestre do Scale Out, \<unidade\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config, no nó Mestre. Atualize **SSLCertThumbprint** para a impressão digital do novo certificado SSL.

#### <a name="4-restart-scale-out-master-service"></a>4. Reiniciar o serviço do Mestre do Scale Out

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Reconectar o Trabalho do Scale Out ao Mestre do Scale Out
Para cada Trabalho do Scale Out, exclua o Trabalho e adicione-o novamente com o [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md) ou então siga as etapas 5.1 a 5.3 abaixo:

5.1 Instalar o certificado SSL do cliente ao repositório raiz do computador local no nó de trabalho

5.2 Atualizar o arquivo de configuração de serviço de Trabalho do Scale Out, \<unidade\>:\Arquivos de Programas\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config, no nó de Trabalho. Atualize **MasterHttpsCertThumbprint** para a impressão digital do novo certificado SSL.

5.3 Reiniciar o serviço de Trabalho do Scale Out


## <a name="scale-out-worker-certificate"></a>Certificado de Trabalho do Scale Out

Durante a instalação do Trabalho do Scale Out, o respectivo certificado é gerado automaticamente. 

### <a name="change-scale-out-worker-certificate"></a>Alterar certificado de Trabalho do Scale Out

Caso você deseje alterar o certificado de Trabalho do Scale Out, siga as etapas abaixo.

#### <a name="1-create-a-certificate"></a>1. Criar um certificado
Crie e instale um certificado com o seguinte comando:
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
Exemplo:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. Instalar o certificado do cliente no repositório raiz do computador local no nó de trabalho

#### <a name="3-give-service-access-to-the-certificate"></a>3. Conceder acesso ao certificado para o serviço
Exclua o certificado antigo e conceda acesso ao novo certificado ao serviço do Trabalho do Scale Out com o comando:
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
Exemplo:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Atualizar arquivo de configuração do Trabalho do Scale Out
Atualize o arquivo de configuração de serviço de Trabalho do Scale Out, \<unidade\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config, no nó do Trabalho. Atualize **WorkerHttpsCertThumbprint** para a impressão digital do novo certificado.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. Instalar o certificado do cliente no repositório raiz do computador local no nó Mestre

#### <a name="6-restart-scale-out-worker-service"></a>6. Reiniciar o serviço Trabalho do Scale Out
