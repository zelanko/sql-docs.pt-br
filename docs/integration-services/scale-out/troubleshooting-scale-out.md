---
title: "Solução de problemas do SSIS (SQL Server Integration Services) Scale Out | Microsoft Docs"
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
ms.openlocfilehash: 56d61bc6ba76514ba2291243002a7423ec8e265c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-scale-out"></a>Solução de problemas do Scale Out

O SSIS Scale Out envolve comunicação entre SSISDB, serviço Mestre do Scale Out e serviço de Trabalho do Scale Out. Às vezes, a comunicação é interrompida devido a erros de configuração, falta de permissões de acesso e outros motivos. Este documento ajuda você a solucionar problemas de sua configuração do Scale Out.

Para investigar os sintomas que você encontrar, siga as etapas abaixo uma a uma até que o problema seja resolvido.

### <a name="symptoms"></a>**Sintomas** 
O Mestre do Scale Out não é capaz de se conectar ao SSISDB. 

Não é possível mostrar as propriedades do Mestre Gerenciador do Scale Out.

As propriedades do Mestre não estão preenchidas em [SSISDB].[catalog].[master_properties]

### <a name="solution"></a>**Solução**
Etapa 1: verifique se o Scale Out está habilitado.

Clique com o botão direito do mouse no nó **SSISDB** no Pesquisador de Objetos do SSMS e marque **O recurso Scale Out está habilitado**.

![O Scale Out está habilitado](media\isenabled.PNG)

Se o valor da propriedade é False, habilite o Scale Out chamando o procedimento armazenado [SSISDB].[catalog].[enable_scaleout].

Etapa 2: verifique se o nome do SQL Server especificado no arquivo de configuração do Mestre do Scale Out está correto e reinicie o serviço do Mestre do Scale Out.

### <a name="symptoms"></a>**Sintomas** 
O Trabalho do Scale Out não é capaz de se conectar ao Mestre do Scale Out

O Trabalho do Scale Out não aparece após ser adicionado ao Gerenciador do Scale Out

O Trabalho do Scale Out não aparece em [SSISDB].[catalog].[worker_agents]

O serviço de Trabalho do Scale Out está em execução, enquanto o Trabalho do Scale Out está offline

### <a name="solutions"></a>**Soluções** 
Verifique as mensagens de erro no log do serviço do Trabalho de Scale Out em \<unidade\>:\Users\\*[conta executando o serviço de trabalho]*\AppData\Local\SSIS\Cluster\Agent.

**Caso** 

System.ServiceModel.EndpointNotFoundException: não houve nenhum ponto de extremidade escutando em https://*[NomeDoComputador]:[Porta]*/ClusterManagement/ que pudesse aceitar a mensagem.

Etapa 1: verifique se o número da porta especificado no arquivo de configuração de serviço do Mestre do Scale Out está correto e reinicie o serviço do Mestre do Scale Out. 

Etapa 2: verifique se o ponto de extremidade mestre especificado no arquivo de configuração de serviço de Trabalho do Scale Out está correto e reinicie o serviço do Trabalho do Scale Out.

Etapa 3: verifique se a porta de firewall está aberta no nó Mestre do Scale Out.

Etapa 4: resolva quaisquer outros problemas de conexão entre o nó Mestre do Scale Out e o nó do Trabalho do Scale Out.

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: não foi possível estabelecer relação de confiança para o canal seguro de SSL/TLS com autoridade '*[Nome do Computador]:[Porta]*'. ---> System.Net.WebException: a conexão subjacente estava fechada: não foi possível estabelecer relação de confiança para o canal seguro de SSL/TLS. ---> System.Security.Authentication.AuthenticationException: o certificado remoto é inválido de acordo com o procedimento de validação.

Etapa 1: instale o certificado do Mestre do Scale Out no repositório de certificados raiz do computador local no nó de Trabalho do Scale Out se ainda não tiver sido instalado e reinicie o serviço de Trabalho do Scale Out.

Etapa 2: verifique se o nome do host no ponto de extremidade mestre está incluído nos CNs do certificado do Mestre do Scale Out. Caso contrário, redefina o ponto de extremidade mestre no arquivo de configuração de Trabalho do Scale Out e reinicie o serviço de Trabalho do Scale Out. 

> [!Note]
> Se não for possível alterar o nome do host do ponto de extremidade mestre devido a configurações de DNS, você precisará alterar o certificado do Mestre do Scale Out. Veja [Lidar com certificados no SSIS Scale Out](deal-with-certificates-in-ssis-scale-out.md).

Etapa 3: verifique se a impressão digital do mestre especificada na configuração do Trabalho do Scale Out corresponde à impressão digital do certificado do Mestre do Scale Out. 

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: não foi possível estabelecer um canal seguro para SSL/TLS com autoridade '*[Nome do Computador]:[Porta]*'. ---> System.Net.WebException: a solicitação foi anulada: não foi possível criar um canal seguro de SSL/TLS.

Etapa 1: verifique se a conta que executa o serviço de Trabalho do Scale Out tem acesso ao certificado de Trabalho do Scale Out usando o comando a seguir.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Se a conta não tem acesso, conceda-o usando o comando abaixo e reinicie o serviço de Trabalho do Scale Out.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**Caso**

System.ServiceModel.Security.MessageSecurityException: a solicitação HTTP foi proibida com um esquema de autenticação de cliente 'Anônimo'. ---> System.Net.WebException: o servidor remoto retornou um erro: (403) Proibido.

Etapa 1: instale o certificado do Trabalho do Scale Out no repositório de certificados raiz do computador local no nó Mestre do Scale Out se ainda não tiver sido instalado e reinicie o serviço de Trabalho do Scale Out.

Etapa 2: limpe certificados inúteis no repositório de certificados raiz do computador local no nó Mestre do Scale Out.

Etapa 3: configure o Schannel para não enviar mais a lista de autoridades de certificação confiáveis durante o processo de handshake TLS/SSL, adicionando a entrada do Registro abaixo no nó Mestre do Scale Out.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Nome do valor: SendTrustedIssuerList 

Tipo de valor: REG_DWORD 

Dados do valor: 0 (False)

**Caso**

System.ServiceModel.CommunicationException: ocorreu um erro ao fazer a solicitação HTTP para https://*[Nome do computador]:[Porta]*/ClusterManagement/. Isso pode ser devido ao fato de que o certificado do servidor não está configurado corretamente com HTTP.SYS no caso HTTPS. Isso também pode ser causado por uma incompatibilidade da associação de segurança entre o cliente e o servidor. 

Etapa 1: verifique se o certificado do Mestre do Scale Out está associado à porta no ponto de extremidade mestre corretamente no nó mestre com o comando abaixo. Verifique se o hash de certificado exibido é correspondido à impressão digital do certificado do Mestre do Scale Out.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Se a associação não estiver correta, redefina-a com os comandos a seguir e reinicie o serviço de Trabalho do Scale Out.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**Sintomas**
Falha na validação ao conectar o Trabalho do Scale Out ao Mestre do Scale Out no Gerenciador do Scale Out com a mensagem de erro "Não é possível abrir o repositório de certificados no computador".

### <a name="solution"></a>**Solução**

Etapa 1: execute o Gerenciador do Scale Out como administrador. Se você abri-lo com o SSMS, você precisará executar o SSMS como administrador.

Etapa 2: inicie o Serviço Registro Remoto no computador se ele não estiver em execução.

### <a name="symptoms"></a>**Sintomas**
A execução no Scale Out não inicia.

### <a name="solution"></a>**Solução**

Verifique o status das máquinas selecionadas para executar o pacote em [SSISDB].[catalog].[worker_agents]. Pelo menos um trabalho deve estar online e habilitado.

### <a name="symptoms"></a>**Sintomas** 
Os pacotes são executados com êxito, mas não há nenhuma mensagem registrada em log.

### <a name="solution"></a>**Solução**

Verifique se a autenticação do SQL Server é permitida pelo SQL Server que hospeda o SSISDB.

> [!Note]  
> Se você alterou a conta para registro em log do Scale Out, consulte [Alterar a conta para registro em log do Scale Out](change-logdb-account.md) e verifique a cadeia de conexão usada para registro em log.

### <a name="symptoms"></a>**Sintomas**
As mensagens de erro no relatório de execução do pacote não são suficientes para solucionar os problemas.

### <a name="solution"></a>**Solução**
Mais logs de execução podem ser encontrados em TasksRootFolder, configurado no WorkerSettings.config. Por padrão, ele é \<unidade\>:\Users\\*[conta]*\AppData\Local\SSIS\ScaleOut\Tasks. *[conta]* é a conta que executa o serviço do Trabalho do Scale Out com o valor padrão SSISScaleOutWorker140.

Para localizar o log para a execução do pacote com a *[ID de execução]*, execute o comando T-SQL abaixo para obter a *[ID da tarefa]*. Em seguida, localize a subpasta nomeada com *[ID da tarefa]* em TasksRootFolder.<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> Essa consulta é para a finalidade exclusiva de solucionar problemas e estará aberta a alterações quando o cenário de registro em log/diagnóstico do Trabalho do Scale Out for aprimorado no futuro. 
