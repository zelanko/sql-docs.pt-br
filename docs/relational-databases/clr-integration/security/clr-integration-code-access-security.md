---
title: Segurança de acesso do código de integração de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cc9d9c90e260fe3da8640189a8a16af15b984769
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35702927"
---
# <a name="clr-integration-code-access-security"></a>Segurança de acesso a código da integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O CLR (common language runtime) dá suporte a um modelo de segurança denominado segurança de acesso para código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Para obter mais informações, consulte a seção "Segurança de acesso do código" no Software Development Kit do .NET Framework.  
  
 A política de segurança que determina as permissões concedidas a assemblies é definida em três locais diferentes:  
  
-   Política de máquina: trata-se da política em vigor para todo o código gerenciado em execução na máquina na qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado.  
  
-   Política de usuário: trata-se da política em vigor para o código gerenciado hospedado por um processo. No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a política de usuário é específica da conta do Windows na qual o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está em execução.  
  
-   Política de host: trata-se da política configurada pelo host do CLR (nesse caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) em vigor para o código gerenciado em execução no host.  
  
 O mecanismo da segurança de acesso do código para o qual o CLR oferece suporte se baseia na pressuposição de que o tempo de execução pode hospedar tanto o código totalmente confiável quanto o parcialmente confiável. Os recursos que são protegidos pela segurança de acesso do código CLR costumam estar em interfaces de programação de aplicativo gerenciado que exigem a permissão correspondente antes de permitir o acesso ao recurso. A demanda para a permissão é satisfatória apenas quando todos os chamadores (no nível de assembly) na pilha de chamadas tiverem a permissão do recurso correspondente.  
  
 O conjunto de permissões da segurança de acesso do código concedidas ao código gerenciado em execução no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é a interseção do conjunto de permissões concedidas pelos três níveis de política acima. Mesmo que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conceda um conjunto de permissões a um assembly carregado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o conjunto de permissões final dado ao código do usuário pode ser restringido ainda mais com as políticas de nível do usuário e da máquina.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permissões do nível de política do host do SQL Server  
 O conjunto de permissões da segurança de acesso do código concedidas a assemblies pelo nível de política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é determinado pelo conjunto de permissões especificado durante a criação do assembly. Há três conjuntos de permissão: **seguro**, **EXTERNAL_ACCESS** e **UNSAFE** (especificada usando o **PERMISSION_SET** opção de [ Criar ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece um nível de política de segurança em nível de host ao CLR ao hospedá-lo; essa política é um nível de política adicional abaixo dos dois níveis de política que estão sempre em vigor. Essa política é definida para todos os domínios de aplicativo criados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essa política não se destina ao domínio de aplicativo padrão que entraria em vigor quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criasse uma instância do CLR.  
  
 A política de nível host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma combinação de política fixa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para assemblies de sistema e política específica de usuário para assemblies de usuário.  
  
 A política fixa para assemblies do CLR e assemblies de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a eles confiança total.  
  
 A parte especificada pelo usuário da política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se baseia na especificação de um dos três recipientes de permissão para cada assembly pelo proprietário do assembly. Para obter mais informações sobre as permissões de segurança listadas abaixo, consulte o SDK do .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Somente a computação interna e o acesso a dados local são permitidos. **SEGURANÇA** é o conjunto de permissões mais restritivo. O código executado por um assembly com **seguro** permissões não podem acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou registro.  
  
 **SEGURANÇA** assemblies têm as permissões e os valores a seguir:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Execução:** permissão para executar código gerenciado.|  
|**SqlClientPermission**|**Conexão de contexto = true**, **conexão de contexto = yes**: apenas a conexão de contexto pode ser usado e a cadeia de caracteres de conexão só pode especificar um valor de "conexão de contexto = true" ou "conexão de contexto = yes".<br /><br /> **AllowBlankPassword = false:** não são permitidas senhas em branco.|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Assemblies EXTERNAL_ACCESS têm as mesmas permissões **seguro** assemblies, com a capacidade adicional para acessar recursos externos do sistema, como arquivos, redes, variáveis de ambiente e o registro.  
  
 **EXTERNAL_ACCESS** assemblies também têm as permissões e os valores a seguir:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Irrestrito:** transações distribuídas são permitidas.|  
|**DNSPermission**|**Irrestrito:** permissão para solicitar informações de servidores de nome de domínio.|  
|**EnvironmentPermission**|**Irrestrito:** completo é permitido o acesso a variáveis de ambiente do sistema e do usuário.|  
|**EventLogPermission**|**Administrar:** as seguintes ações são permitidas: criar uma fonte de evento, ler logs existentes, excluir origens do evento ou logs, responder a consultas, limpar um log de eventos, escutar eventos e acessar uma coleção de todos os logs de eventos.|  
|**FileIOPermission**|**Irrestrito:** acesso completo a arquivos e pastas é permitido.|  
|**KeyContainerPermission**|**Irrestrito:** completo é permitido o acesso a contêineres de chave.|  
|**NetworkInformationPermission**|**Acesso:** Pinging é permitido.|  
|**RegistryPermission**|Permite que o direito de leitura **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**e  **HKEY_USERS.**|  
|**SecurityPermission**|**Asserção:** capacidade de declarar que todos os chamadores do código tenham a permissão necessária para a operação.<br /><br /> **ControlPrincipal:** capacidade de manipular o objeto principal.<br /><br /> **Execução:** permissão para executar código gerenciado.<br /><br /> **ComoSerializationFormatter:** capacidade de fornecer serviços de serialização.|  
|**SmtpPermission**|**Acesso:** são permitidas conexões de saída para a porta de host SMTP 25.|  
|**SocketPermission**|**Conecte-se:** são permitidas conexões de saída (todas as portas, todos os protocolos) em um endereço de transporte.|  
|**SqlClientPermission**|**Irrestrito:** total acesso à fonte de dados é permitido.|  
|**StorePermission**|**Irrestrito:** acesso completo para o certificado x. 509 repositórios é permitido.|  
|**WebPermission**|**Conecte-se:** são permitidas conexões de saída para recursos da web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite que os assemblies tenham acesso irrestrito aos recursos, dentro e fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Código em execução em um **UNSAFE** assembly também pode chamar código não gerenciado.  
  
 **UNSAFE** assemblies recebem **FullTrust**.  
  
> [!IMPORTANT]  
>  **SEGURANÇA** é a configuração de permissão recomendada para assemblies que executam tarefas de gerenciamento de computação e dados sem acessar recursos externos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** é recomendada para assemblies que acessam recursos fora [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** assemblies por padrão são executados como a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta de serviço. É possível **EXTERNAL_ACCESS** código representar explicitamente o contexto de segurança de autenticação do Windows do chamador. Como o padrão é executar como a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta de serviço, permissão para executar **EXTERNAL_ACCESS** deve ser fornecida apenas para logons confiados para execução como a conta de serviço. De uma perspectiva de segurança, **EXTERNAL_ACCESS** e **UNSAFE** assemblies forem idênticos. No entanto, **EXTERNAL_ACCESS** assemblies fornecem várias proteções de confiabilidade e robustez que não estão na **UNSAFE** assemblies. Especificando **UNSAFE** permite que o código do assembly execute operações ilegais no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] espaço de processo e portanto pode comprometer potencialmente a robustez e a escalabilidade de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como criar assemblies CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Gerenciando Assemblies de integração de CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Acessando recursos externos  
 Se um tipo definido pelo usuário (UDT), procedimento armazenado ou outro tipo de construção for registrado com o **seguro** conjunto de permissões e código gerenciado em execução na construção não é capaz de acessar recursos externos. No entanto, se o **EXTERNAL_ACCESS** ou **UNSAFE** conjuntos de permissões são especificados e código gerenciado tenta acessar recursos externos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica as seguintes regras:  
  
|Se|Então|  
|--------|----------|  
|O contexto de execução corresponda a um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|As tentativas de acessar recursos externos são negadas, e ocorre uma exceção de segurança.|  
|O contexto de execução corresponda a um logon do Windows e seja o chamador original.|O recurso externo é acesso no contexto de segurança da conta do serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|O chamador não for o chamador original.|O acesso será negado, e ocorrerá uma exceção de segurança.|  
|O contexto de execução corresponder a um logon do Windows e o contexto da execução for o chamador original, e o chamador tiver sido representado.|O acesso usará o contexto de segurança do chamador, não a conta de serviço.|  
  
## <a name="permission-set-summary"></a>Resumo do conjunto de permissões  
 O gráfico a seguir resume as restrições e permissões concedidas para o **seguro**, **EXTERNAL_ACCESS**, e **UNSAFE** conjuntos de permissões.  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**NÃO SEGURO**|  
|**Permissões de segurança de acesso do código**|Somente execução|Execução + acesso a recursos externos|Irrestrito (inclusive P/Invoke)|  
|**Restrições do modelo de programação**|Sim|Sim|Sem restrições|  
|**Requisito de verificabilidade**|Sim|Sim|não|  
|**Acesso a dados locais**|Sim|Sim|Sim|  
|**Capacidade de chamar código nativo**|não|não|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Segurança da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Atributos de proteção de host e programação da integração CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrições do modelo de programação de integração de CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente hospedado de CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
