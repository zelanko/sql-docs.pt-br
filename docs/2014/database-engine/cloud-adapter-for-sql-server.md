---
title: Adaptador de nuvem para o SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cloud adapter
- Deploy to Windows Azure
ms.assetid: 82ed0d0f-952d-4d49-aa36-3855a3ca9877
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2ddaf87aa91e62cc422bf5a4558232f03339121
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065151"
---
# <a name="cloud-adapter-for-sql-server"></a>Adaptador de nuvem para SQL Server
  O serviço de Adaptador de Nuvem é criado como parte do provisionamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em uma máquina virtual do Windows Azure. O serviço de Adaptador de Nuvem gera um certificado SSL autoassinado como parte da sua primeira execução e é executado como uma conta **Sistema Local** . Ele gera um arquivo de configuração que é usado para autoconfiguração. O Adaptador de Nuvem também cria uma regra de Firewall do Windows para permitir suas conexões TCP de entrada na porta padrão 11435.  
  
 O Adaptador de Nuvem é um serviço síncrono sem monitoração de estado que recebe mensagens da instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando o serviço de Adaptador de Nuvem é interrompido, ele interrompe o Adaptador de Nuvem de acesso remoto, desassocia o certificado SSL e desabilita a regra de Firewall do Windows.  
  
## <a name="cloud-adapter-requirements"></a>Requisitos do Adaptador de Nuvem  
 Observe os requisitos a seguir para instalação, habilitação e execução do Adaptador de Nuvem para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   O Adaptador de Nuvem tem suporte com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 e superior. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012, o Adaptador de Nuvem para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exige SQL Management Objects para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012.  
  
-   O serviço Web do Adaptador de Nuvem é executado como uma conta **Sistema Local** e verifica as credenciais do cliente antes de executar qualquer tarefa. As credenciais fornecidas pelo cliente devem pertencer à conta do usuário que seja membro do local **administradores** grupo no computador remoto.  
  
-   O Adaptador de Nuvem oferece suporte somente à Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   O Adaptador de Nuvem usa a conta do administrador local da VM para executar comandos no computador local, e não uma conta sa.  
  
-   O Adaptador de Nuvem escuta em TCP/IP. A porta padrão é 11435.  
  
-   O Adaptador de Nuvem deve ter permissões para criar e modificar regras de Firewall do Windows.  
  
## <a name="cloud-adapter-configuration-settings"></a>Definições de configuração do Adaptador de Nuvem  
 Use os detalhes de configuração a seguir para modificar as configurações de um Adaptador de Nuvem.  
  
-   **Caminho padrão para o arquivo de configuração** -C:\Program Files\Microsoft SQL Server\120\Tools\CloudAdapter\  
  
-   **Parâmetros do arquivo de configuração** -  
  
    -   \<configuration>  
  
        -   \<appSettings>  
  
            -   \<add key="WebServicePort" value="" />  
  
            -   \<add key="WebServiceCertificate" value="GUID" />  
  
            -   \<add key="ExposeExceptionDetails" value="true" />  
  
        -   \</appSettings>  
  
    -   \</configuration>  
  
-   **Detalhes do certificado** -o certificado tem os seguintes valores:  
  
    -   Subject - "CN=CloudAdapter\<VMName>, DC=SQL Server, DC=Microsoft"  
  
    -   O certificado deve ter somente o EKU da Autenticação do Servidor habilitado.  
  
    -   O comprimento da chave do certificado é de 2048.  
  
 **Valores do arquivo de configuração**:  
  
|Configuração|Valores|Padrão|Comentários|  
|-------------|------------|-------------|--------------|  
|WebServicePort|1-65535|11435|Se não for especificada, use 11435.|  
|WebServiceCertificate|Impressão digital|Empty (vazio)|Se estiver vazio, um novo certificado autoassinado será gerado.|  
|ExposeExceptionDetails|True/False|Falso||  
  
## <a name="cloud-adapter-troubleshooting"></a>Solução de problemas do Adaptador de Nuvem  
 Use as informações a seguir para solucionar problemas do Adaptador de Nuvem para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Tratamento de erros e registro em log** -mensagens de status e erros são gravadas no Log de eventos do aplicativo.  
  
-   **Rastreamento, eventos** -todos os eventos são gravados no Log de eventos do aplicativo.  
  
-   **Controle, configuração** -Use o arquivo de configuração localizado em:  C:\Program Files\Microsoft SQL Server\120\Tools\CloudAdapter\\.  
  
|Erro|ID do erro|Causa|Resolução|  
|-----------|--------------|-----------|----------------|  
|Houve uma exceção ao adicionar o certificado ao repositório de certificados. {Texto da exceção}.|45560|Permissões do repositório de certificados de máquina|Certifique-se de que o serviço de adaptador de nuvem tem permissões para adicionar certificados ao repositório de certificados do computador.|  
|Houve uma exceção ao tentar configurar a associação SSL para a porta {número da porta} e o certificado {impressão digital}. {Exceção}.|45561|Outro aplicativo já usou a porta ou associou um certificado a ela.|Remova as associações existentes ou altere a porta do Adaptador de Nuvem no arquivo de configuração.|  
|Falha ao localizar o certificado SSL [{Impressão digital}] no repositório de certificados.|45564|A impressão digital do certificado está no arquivo de configuração, mas o repositório de certificados pessoal para o serviço não contém certificados.<br /><br /> Permissões insuficientes|Verifique se o certificado está no repositório de certificados pessoal do serviço.<br /><br /> Verifique se o serviço tem as permissões corretas para o repositório.|  
|Falha ao iniciar o serviço Web. {Texto da exceção}.|45570|Descrito na exceção.|Habilite ExposeExceptionDetails e use as informações estendidas da exceção.|  
|O certificado [{Impressão digital}] expirou.|45565|Certificado expirado fazia referência do arquivo de configuração.|Adicione um certificado válido e atualize o arquivo de configuração com a respectiva impressão digital.|  
|Erro do serviço Web: {0}.|45571|Descrito na exceção.|Habilite ExposeExceptionDetails e use as informações estendidas da exceção.|  
  
## <a name="see-also"></a>Consulte também  
 [Implantar um banco de dados do SQL Server em uma máquina virtual do Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)  
  
  
