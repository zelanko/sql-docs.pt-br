---
title: Solucionar problemas de SSIS Scale Out | Microsoft Docs
description: Este artigo descreve como solucionar problemas comuns com o SSIS Scale Out
ms.custom: performance
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 987217c1afe07b5e917f415b9a5bc0d784ab7c6d
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903762"
---
# <a name="troubleshoot-scale-out"></a>Solução de problemas do Scale Out

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



O SSIS Scale Out envolve a comunicação entre o banco de dados do Catálogo do SSIS `SSISDB`, o serviço Mestre do Scale Out e o serviço Trabalho do Scale Out. Às vezes, essa comunicação é interrompida devido a erros de configuração, falta de permissões de acesso e outros motivos. Este artigo ajuda você a solucionar problemas com a configuração do Scale Out.

Para investigar os sintomas que você encontrar, siga as etapas abaixo uma a uma até que o problema seja resolvido.

## <a name="scale-out-master-fails"></a>Falha do Mestre do Scale Out

### <a name="symptoms"></a>Sintomas 
-   O Mestre do Scale Out não é capaz de se conectar ao SSISDB. 

-   Não é possível mostrar as propriedades do Mestre Gerenciador do Scale Out.

-   As propriedades do Mestre não são populadas na exibição `[catalog].[master_properties]`.

### <a name="solution"></a>Solução
1.  Verifique se o Scale Out está habilitado.

    No SSMS, no Pesquisador de Objetos, clique com o botão direito do mouse em **SSISDB** e verifique se o **recurso Scale Out está habilitado**.

    ![O Scale Out está habilitado](media/isenabled.PNG)

    Se o valor da propriedade for False, habilite o Scale Out chamando o procedimento armazenado `[catalog].[enable_scaleout]`.

2.  Verifique se o nome do SQL Server especificado no arquivo de configuração do Mestre do Scale Out está correto e reinicie o serviço Mestre do Scale Out.

## <a name="scale-out-worker-fails"></a>Falha do Trabalho do Scale Out

### <a name="symptoms"></a>Sintomas 
-   O Trabalho do Scale Out não pode se conectar ao Mestre do Scale Out.

-   O Trabalho do Scale Out não é mostrado depois de ser adicionado no Gerenciador do Scale Out.

-   O Trabalho do Scale Out não é mostrado na exibição `[catalog].[worker_agents]`.

-   O serviço Trabalho do Scale Out está em execução, mas o Trabalho do Scale Out está offline.

### <a name="solution"></a>Solução
Verifique as mensagens de erro no log do serviço do Trabalho do Scale Out em `\<drive\>:\Users\\*[account running worker service]*\AppData\Local\SSIS\Cluster\Agent`.

## <a name="no-endpoint-listening"></a>Nenhuma escuta do ponto de extremidade

### <a name="symptoms"></a>Sintomas

*"System.ServiceModel.EndpointNotFoundException: Não havia nenhum ponto de extremidade escutando em https://* [NomeDoComputador]:[Porta] */ClusterManagement/ que pudesse aceitar a mensagem. "*

### <a name="solution"></a>Solução

1.  Verifique se o número da porta especificado no arquivo de configuração de serviço do Mestre do Scale Out está correto e reinicie o serviço Mestre do Scale Out. 

2.  Verifique se o ponto de extremidade mestre especificado no arquivo de configuração de serviço do Trabalho do Scale Out está correto e reinicie o serviço Trabalho do Scale Out.

3.  Verifique se a porta do firewall está aberta no nó Mestre do Scale Out.

4.  Resolva quaisquer outros problemas de conexão entre o nó Mestre do Scale Out e o nó de Trabalho do Scale Out.

## <a name="could-not-establish-trust-relationship"></a>Não foi possível estabelecer a relação de confiança

### <a name="symptoms"></a>Sintomas
*""System.ServiceModel.Security.SecurityNegotiationException: Não foi possível estabelecer a relação de confiança para o canal seguro de SSL/TLS com autoridade '[Nome do Computador]:[Porta]'. "*

*"System.Net.WebException: A conexão subjacente estava fechada: Não foi possível estabelecer relação de confiança para o canal seguro SSL/TLS."*

*"System.Security.Authentication.AuthenticationException: O certificado remoto é inválido de acordo com o procedimento de validação."*

### <a name="solution"></a>Solução
1.  Instale o certificado do Mestre do Scale Out no repositório de certificados Raiz do computador local no nó de Trabalho do Scale Out, caso o certificado ainda não esteja instalado e reinicie o serviço Trabalho do Scale Out.

2.  Verifique se o nome do host no ponto de extremidade mestre está incluído nos CNs do certificado do Mestre do Scale Out. Caso contrário, redefina o ponto de extremidade mestre no arquivo de configuração do Trabalho do Scale Out e reinicie o serviço Trabalho do Scale Out. 

    > [!NOTE]
    > Se não for possível alterar o nome do host do ponto de extremidade mestre devido a configurações de DNS, você precisará alterar o certificado do Mestre do Scale Out. Consulte [Gerenciar certificados para o SSIS Scale Out](deal-with-certificates-in-ssis-scale-out.md).

3.  Verifique se a impressão digital mestre especificada na configuração do Trabalho do Scale Out corresponde à impressão digital do certificado do Mestre do Scale Out. 

## <a name="could-not-establish-secure-channel"></a>Não foi possível estabelecer um canal de segurança

### <a name="symptoms"></a>Sintomas

*"System.ServiceModel.Security.SecurityNegotiationException: Não foi possível estabelecer um canal seguro para SSL/TLS com autoridade '[Nome do Computador]:[Porta]'."*

*"System.Net.WebException: A solicitação foi anulada: Não foi possível criar um canal seguro SSL/TLS."*

### <a name="solution"></a>Solução
Verifique se a conta que executa o serviço Trabalho do Scale Out tem acesso ao certificado do Trabalho do Scale Out executando o seguinte comando:

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Se a conta não tiver acesso, conceda acesso a ela executando o comando a seguir e reinicie o serviço Trabalhador do Scale Out.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

## <a name="http-request-forbidden"></a>Solicitação HTTP proibida

### <a name="symptoms"></a>Sintomas

*"System.ServiceModel.Security.MessageSecurityException: A solicitação HTTP foi proibida com o esquema de autenticação cliente 'Anônimo'."*

*"System.Net.WebException: O servidor remoto retornou um erro: (403) Proibido."*

### <a name="solution"></a>Solução
1.  Instale o certificado do Trabalho do Scale Out no repositório de certificados Raiz do computador local no nó Mestre do Scale Out, caso o certificado ainda não esteja instalado e reinicie o serviço Trabalho do Scale Out.

2.  Limpe os certificados inúteis no repositório de certificados Raiz do computador local no nó Mestre do Scale Out.

3.  Configure o Schannel para não enviar mais a lista de autoridades de certificação confiáveis durante o processo de handshake TLS/SSL adicionando a entrada do Registro a seguir ao nó Mestre do Scale Out.

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    Nome do valor: **SendTrustedIssuerList** 

    Tipo de valor: **REG_DWORD** 

    Dados do valor: **0 (Falso)**

4.  Se não for possível limpar todos os certificados não autoassinados, conforme descrito na etapa 2, defina o valor da chave do Registro a seguir como 2.

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    Nome do valor: **ClientAuthTrustMode** 

    Tipo de valor: **REG_DWORD** 

    Dados do valor: **2**

    > [!NOTE]
    > Se você tiver certificados não autoassinados no repositório de certificados raiz, a autenticação de certificado do cliente falhará. Para saber mais, confira [Os Serviços de Informações da Internet (IIS) 8 podem rejeitar solicitações de certificado de cliente com erros HTTP 403.7 ou 403.16](https://support.microsoft.com/help/2802568/internet-information-services-iis-8-may-reject-client-certificate-requ).

## <a name="http-request-error"></a>Erro de solicitação HTTP

### <a name="symptoms"></a>Sintomas

*"System.ServiceModel.CommunicationException: Ocorreu um erro ao fazer a solicitação HTTP para https://[Nome do Computador]:[Porta]/ClusterManagement/. Isso pode ser devido ao fato de que o certificado do servidor não está configurado corretamente com HTTP.SYS no caso HTTPS. Isso também pode ser causado por uma incompatibilidade da associação de segurança entre o cliente e o servidor.”*

### <a name="solution"></a>Solução
1.  Verifique se o certificado do Mestre do Scale Out está associado à porta no ponto de extremidade mestre corretamente do nó mestre executando o seguinte comando:

    ```dos
    netsh http show sslcert ipport=0.0.0.0:{Master port}
    ```

    Verifique se o hash de certificado exibido corresponde à impressão digital do certificado do Mestre do Scale Out. Se a associação não estiver correta, redefina-a executando os comandos a seguir e reinicie o serviço Trabalho do Scale Out.

    ```dos
    netsh http delete sslcert ipport=0.0.0.0:{Master port}
    netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root  appid={random guid}
    ```

## <a name="cannot-open-certificate-store"></a>Não é possível abrir o repositório de certificados

### <a name="symptoms"></a>Sintomas
Falha na validação ao conectar um Trabalho do Scale Out ao Mestre do Scale Out no Gerenciador do Scale Out com a mensagem de erro *“Não é possível abrir o repositório de certificados no computador.”*

### <a name="solution"></a>Solução

1.  Execute o Gerenciador do Scale Out como administrador. Se você abrir o Gerenciador do Scale Out com o SSMS, precisará executar o SSMS como administrador.

2.  Inicie o serviço Registro Remoto no computador caso ele não esteja em execução.

## <a name="execution-doesnt-start"></a>A execução não é iniciada

### <a name="symptoms"></a>Sintomas
A execução no Scale Out não inicia.

### <a name="solution"></a>Solução

Verifique o status dos computadores selecionados para executar o pacote na exibição `[catalog].[worker_agents]`. Pelo menos um trabalho deve estar online e habilitado.

## <a name="no-log"></a>Nenhum log

### <a name="symptoms"></a>Sintomas 
Os pacotes são executados com êxito, mas não há nenhuma mensagem registrada em log.

### <a name="solution"></a>Solução

Verifique se a Autenticação do SQL Server é permitida pela instância do SQL Server que hospeda o SSISDB.

> [!NOTE]  
> Se você alterou a conta para registro em log do Scale Out, consulte [Alterar a conta para registro em log do Scale Out](change-logdb-account.md) e verifique a cadeia de conexão usada para registro em log.

## <a name="error-messages-arent-helpful"></a>As mensagens de erro não são úteis

### <a name="symptoms"></a>Sintomas
As mensagens de erro do relatório de execução de pacote não são suficientes para solucionar os problemas.

### <a name="solution"></a>Solução
Mais logs de execução podem ser encontrados na `TasksRootFolder` configurada em `WorkerSettings.config`. Por padrão, essa pasta é `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks`. A *[account]* é a conta que executa o serviço Trabalho do Scale Out, com o valor padrão `SSISScaleOutWorker140`.

Para localizar o log para a execução de pacote com a *[execution ID]* , execute o comando T-SQL a seguir para obter a *[task ID]* . Em seguida, encontre o nome da subpasta que contém a *[task ID]* em `TasksRootFolder`.

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```

> [!WARNING]
> Essa consulta destina-se apenas à solução de problemas. As exibições internas referenciadas na consulta deverão ser alteradas no futuro. 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte os seguintes artigos sobre como configurar o SSIS Scale Out:
-   [Introdução ao SSIS (Integration Services) Scale Out em um único computador](get-started-with-ssis-scale-out-onebox.md)
-   [Passo a passo: Configurar SSIS (Integration Services) Scale Out](walkthrough-set-up-integration-services-scale-out.md)
