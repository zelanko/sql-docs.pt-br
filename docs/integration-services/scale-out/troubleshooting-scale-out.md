---
title: "Solução de problemas do SQL Server Integration Services (SSIS) de expansão | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41bb853dd08591596f6f5baa918e174d0c26a6b5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-scale-out"></a>Solução de problemas de expansão

SSIS expansão envolve communtication entre SSISDB, escala Out mestre serviço e escala fora do trabalho. Às vezes, a comunicação é interrompida devido a erros de configuração, falta de permissões de acesso e outros motivos. Este documento ajuda você a solucionar problemas de sua configuração de expansão.

Para investigar os sintomas que você encontrar, siga as etapas abaixo uma até que o problema seja resolvido.

### <a name="symptoms"></a>**Sintomas** 
Escala Out mestre não pode se conectar ao SSISDB. 

Não é possível mostrar propriedades principais no Gerenciador de fora da escala.

Propriedades mestres não são preenchidas [SSISDB]. [catalog]. [master_properties]

### <a name="solution"></a>**Solução**
Etapa 1: Verificar se expandir está habilitado.

Clique com botão direito **SSISDB** nó no Pesquisador de objetos do SSMS e marque **expansão está ativado**.

![Expansão esteja](media\isenabled.PNG)

Se o valor da propriedade é False, habilite expansão chamando o procedimento armazenado [SSISDB]. [catalog]. [enable_scaleout].

Etapa 2: Verifique se o nome do Sql Server especificado no arquivo de configuração de escala Out mestre está correto e reinicie o serviço de escala Out mestre.

### <a name="symptoms"></a>**Sintomas** 
Escala Out trabalho não pode se conectar a escala Out mestre

Escala Out trabalhador não mostrar após adicioná-lo no Gerenciador de fora da escala

Escala Out trabalhador não mostrar em [SSISDB]. [catalog]. [worker_agents]

Serviço de escala Out trabalho está em execução, enquanto o escala Out trabalhador está offline

### <a name="solutions"></a>**Soluções** 
Verifique as mensagens de erro no log do serviço de escala Out trabalhador em \<driver\>: \Users\\*[conta que está executando o serviço do trabalhador]*\AppData\Local\SSIS\Cluster\Agent.

**Caso** 

System.ServiceModel.EndpointNotFoundException: não houve nenhum ponto de extremidade escutando em https://*[nome_do_computador]: [porta]*/ClusterManagement/ pode aceitar a mensagem.

Etapa 1: Verifique se o número da porta especificado no arquivo de configuração de serviço de escala Out mestre está correto e reinicie o serviço de escala Out mestre. 

Etapa 2: Verifique se o ponto de extremidade mestre especificado na configuração do serviço de escala Out trabalhador está correto e reinicie o serviço de escala fora do trabalho.

Etapa 3: Verificar se a porta de firewall está aberta no nó de escala Out mestre.

Etapa 4: Resolver quaisquer outros problemas de conexão entre o nó de escala Out mestre e escala fora do trabalho.

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: Não foi possível estabelecer relação de confiança para o canal seguro de SSL/TLS com autoridade '*[nome do computador]: [porta]*'. ---> System.NET. WebException: A conexão subjacente estava fechada: não foi possível estabelecer relação de confiança para o canal seguro de SSL/TLS. ---> System.Security.Authentication.AuthenticationException: O certificado remoto é inválido de acordo com o procedimento de validação.

Etapa 1: Escala Out mestre de instalação de certificado ao repositório de certificados raiz da máquina local no nó de escala Out trabalho se não ainda instalado e reinicie o serviço de escala fora do trabalho.

Etapa 2: Verifique se o nome do host no ponto de extremidade mestre está incluído no certificado CNs de escala Out mestre. Caso contrário, redefina o ponto de extremidade mestre no arquivo de configuração de escala fora do trabalho e reinicie o serviço de escala fora do trabalho. 

> [!Note]
> Se não for possível alterar o nome do host do ponto de extremidade mestre devido a configurações de DNS, você precisa alterar o certificado de escala Out mestre. Consulte [lidar com certificados no SSIS expansão](deal-with-certificates-in-ssis-scale-out.md).

Etapa 3: Verifique se a impressão digital do mestre especificada na configuração de escala Out trabalho corresponde a impressão digital do certificado de escala Out mestre. 

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: Não foi possível estabelecer um canal seguro para SSL/TLS com autoridade '*[nome do computador]: [porta]*'. ---> System.NET. WebException: A solicitação foi anulada: não foi possível criar o canal seguro de SSL/TLS.

Etapa 1: Verificar se a conta que executa o serviço de escala Out trabalho tem acesso ao certificado de escala fora do trabalho, o comando a seguir.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Se a conta não tem acesso, conceda o comando abaixo e reinicie o serviço de escala fora do trabalho.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**Caso**

System.ServiceModel.Security.MessageSecurityException: A solicitação HTTP está proibida com o esquema de autenticação de cliente 'Anonymous'. ---> System.NET. WebException: O servidor remoto retornou um erro: proibido (403).

Etapa 1: Instalar escala Out trabalho certificado ao repositório de certificados raiz do computador local no nó de escala Out mestre se não ainda instalado e reinicie o serviço de escala fora do trabalho.

Etapa 2: Limpe inútil certificados no repositório de certificados raiz do computador local no nó de escala Out mestre.

Etapa 3: Configure o Schannel para não enviar mais a lista de autoridades de certificação raiz confiáveis durante o processo de handshake TLS/SSL, adicionando a entrada de registro abaixo no nó de escala Out mestre.

Hkey_local_machine\system\currentcontrolset\control\securityproviders\schannel.

Nome do valor: SendTrustedIssuerList 

Tipo de valor: REG_DWORD 

Dados do valor: 0 (FALSO)

**Caso**

System.ServiceModel.CommunicationException: Erro ao fazer a solicitação HTTP para https://*[nome do computador]: [porta]*  /ClusterManagement /. Isso pode ser devido ao fato de que o certificado do servidor não está configurado corretamente com HTTP. SYS no caso HTTPS. Isso também pode ser causado por uma incompatibilidade da associação de segurança entre o cliente e o servidor. 

Etapa 1: Verificar se escala Out mestre certificado está associado à porta no ponto de extremidade mestre corretamente no nó principal com o comando a seguir. Verifique se o hash de certificado exibido é correspondido com impressão digital do certificado escala Out mestre.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Se a associação não estiver correta, redefini-lo com os comandos a seguir e reinicie o serviço de escala fora do trabalho.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**Sintomas**
Não iniciar a execução em expansão.

### <a name="solution"></a>**Solução**

Verifique o status das máquinas selecionadas para executar o pacote em [SSISDB]. [catalog]. [worker_agents]. Pelo menos um trabalho deve estar online e habilitada.

### <a name="symptoms"></a>**Sintomas** 
Pacotes executados com êxito, mas não há nenhuma mensagem registrada.

### <a name="solution"></a>**Solução**

Verifique se a autenticação do SQL Server é permitida pelo Sql Server hospeda o SSISDB.

> [!Note]  
> Se você alterou a conta para o log de expansão, consulte [alterar a conta para escala Out log](change-logdb-account.md) e verifique se a cadeia de conexão usada para registro em log.

### <a name="symptoms"></a>**Sintomas**
As mensagens de erro no relatório de execução do pacote não são suficientes para solução de problemas.

### <a name="solution"></a>**Solução**
Mais logs de execução podem ser encontrados em TasksRootFolder configurado no WorkerSettings.config. Por padrão, ele é \<driver\>: \Users\\*[conta]*\AppData\Local\SSIS\ScaleOut\Tasks. O *[conta]* é a conta que executa o serviço de escala fora do trabalho com o valor padrão SSISScaleOutWorker140.

Para localizar o log para a execução do pacote com *[id de execução]*, execute o comando T-SQL abaixo para obter o *[id da tarefa]*. Em seguida, localize a subpasta denominada com *[id da tarefa]* em TasksRootFolder.<sup> 1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> essa consulta é para solucionar problemas de finalidade única e abra alterar quando o cenário de log/diagnóstico escala Out trabalhador foi aprimorado no futuro. 
