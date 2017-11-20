---
title: "Lidar com certificados no Sql Server Integration Services expansão | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2970b2b2cc7cf30c18a203ebbb92b5418bfc9be5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>Lidar com certificados no SQL Server Integration Services expansão

Para proteger a comunicação entre mestre fora de escala e escala fora do trabalho, dois certificados são usados em expansão, ou seja, o certificado de escala Out mestre e escala fora do trabalho. 

## <a name="scale-out-master-certificate"></a>Certificado de escala Out mestre

Na maioria dos casos, o certificado de escala Out mestre está configurado durante a instalação do mestre de fora da escala.

No **escala Out configuração do Integration Services - mestre nó** página do Assistente de instalação do SQL Server, você pode optar por criar um novo certificado SSL autoassinado ou usar um certificado SSL existente.

![Configuração do mestre](media/master-config.PNG)

Se você não tem requisitos especiais em certificados, você pode optar por criar um novo certificado SSL autoassinado. Você também pode especificar o CNs no certificado. Verifique se o nome do host do ponto de extremidade mestre usada posteriormente por operador fora de escala é incluído no CNs. Por padrão, o nome do computador e o ip do nó mestre são incluídos. 

Se você optar por usar um certificado existente, clique em "Procurar..." para selecionar um certificado SSL do **raiz** repositório de certificados do computador local.

### <a name="change-scale-out-master-certificate"></a>Alterar escala Out mestre certificado

Você talvez queira alterar o certificado de escala Out mestre devido à expiração do certificado ou por outros motivos. Siga as etapas abaixo:

#### <a name="1-create-a-ssl-certificate"></a>1. Crie um certificado SSL.
Criar e instalar um certificado SSL no mestre de nó com o seguinte comando:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Exemplo:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. Associe o certificado ao mestre de porta
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
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Atualizar o arquivo de configuração do serviço de escala Out mestre
Arquivo de configuração de serviço de escala Out mestre de atualização, \<driver\>: \Program Files\Microsoft Server\140\DTS\Binn\MasterSettings.config SQL, no mestre de nó. Atualização **SSLCertThumbprint** para a impressão digital do novo certificado SSL.

#### <a name="4-restart-scale-out-master-service"></a>4. Reinicie o serviço de escala Out mestre

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Reconectar-se a expansão de trabalhador para expansão mestre
Para cada escala Out, ou excluir o trabalho e adicioná-la com novamente [escala Out Manager](integration-services-ssis-scale-out-manager.md) ou siga as etapas 5.1 para 5.3 abaixo:

5.1 instalar o certificado SSL do cliente para o repositório raiz da máquina local no nó de trabalho

5.2 atualizar escala Out trabalho serviço configuração arquivo atualização escala Out trabalho serviço arquivo de configuração, \<driver\>: \Program Files\Microsoft Server\140\DTS\Binn\WorkerSettings.config SQL, no nó do operador. Atualização **MasterHttpsCertThumbprint** para a impressão digital do novo certificado SSL.

5.3 reiniciar escala fora do serviço do trabalhador


## <a name="scale-out-worker-certificate"></a>Certificado de escala fora do trabalho

Certificado de escala fora do trabalho é gerado automaticamente durante a instalação da escala fora do trabalho. 

### <a name="change-scale-out-worker-certificate"></a>Alterar o certificado de escala fora do trabalho

Em casos que você deseja alterar o certificado de escala fora do trabalho, siga as etapas abaixo.

#### <a name="1-create-a-certificate"></a>1. Criar um certificado
Crie e instale um certificado com o seguinte comando:
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
Exemplo:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. Instalar o certificado de cliente para o repositório raiz da máquina local no nó de trabalho

#### <a name="3-give-service-access-to-the-certificate"></a>3. Conceder acesso de serviço para o certificado
Excluir o certificado antigo e dar acesso ao serviço de escala fora do trabalho para o novo certificado com o comando:
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
Exemplo:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Arquivo de configuração de escala fora do trabalho de atualização
Arquivo de configuração de serviço de escala fora do trabalho de atualização, \<driver\>: \Program Files\Microsoft Server\140\DTS\Binn\WorkerSettings.config SQL, no nó do operador. Atualização **WorkerHttpsCertThumbprint** para a impressão digital do novo certificado.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. Instalar o certificado de cliente para o repositório raiz da máquina local no mestre de nó

#### <a name="6-restart-scale-out-worker-service"></a>6. Reinicie o serviço de escala fora do trabalho

