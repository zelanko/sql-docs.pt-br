---
title: Segurança de acesso ao código de integração CLR | Microsoft Docs
description: Para SQL Server integração CLR, o CLR dá suporte à segurança de acesso ao código para código gerenciado, em que as permissões são concedidas a assemblies com base na identidade do código.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
ms.openlocfilehash: b2706faaf181e609df6209758e60b2a46c87aa46
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248614"
---
# <a name="clr-integration-code-access-security"></a>Segurança de acesso a código da integração CLR
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  O CLR (common language runtime) dá suporte a um modelo de segurança denominado segurança de acesso para código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Para obter mais informações, consulte a seção "Segurança de acesso do código" no Software Development Kit do .NET Framework.  
  
 A política de segurança que determina as permissões concedidas a assemblies é definida em três locais diferentes:  
  
-   Política de máquina: trata-se da política em vigor para todo o código gerenciado em execução na máquina na qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado.  
  
-   Política de usuário: trata-se da política em vigor para o código gerenciado hospedado por um processo. No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a política de usuário é específica da conta do Windows na qual o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está em execução.  
  
-   Política de host: trata-se da política configurada pelo host do CLR (nesse caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) em vigor para o código gerenciado em execução no host.  
  
 O mecanismo da segurança de acesso do código para o qual o CLR oferece suporte se baseia na pressuposição de que o runtime pode hospedar tanto o código totalmente confiável quanto o parcialmente confiável. Os recursos protegidos pela segurança de acesso do código do CLR costumam estar em interfaces de programação de aplicativo gerenciadas que exigem  a permissão correspondente para permitir o acesso ao recurso. A demanda para a permissão é satisfatória apenas quando todos os chamadores (no nível de assembly) na pilha de chamadas tiverem a permissão do recurso correspondente.  
  
 O conjunto de permissões da segurança de acesso do código concedidas ao código gerenciado em execução no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é a interseção do conjunto de permissões concedidas pelos três níveis de política acima. Mesmo que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conceda um conjunto de permissões a um assembly carregado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o conjunto de permissões final dado ao código do usuário pode ser restringido ainda mais com as políticas de nível do usuário e da máquina.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permissões do nível de política do host do SQL Server  
 O conjunto de permissões da segurança de acesso do código concedidas a assemblies pelo nível de política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é determinado pelo conjunto de permissões especificado durante a criação do assembly. Há três conjuntos de permissões: **seguro**, **EXTERNAL_ACCESS** e **não seguro** (especificado usando a opção **PERMISSION_SET** de [Create assembly &#40;Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece um nível de política de segurança em nível de host ao CLR ao hospedá-lo; essa política é um nível de política adicional abaixo dos dois níveis de política que estão sempre em vigor. Essa política é definida para todos os domínios de aplicativo criados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essa política não se destina ao domínio de aplicativo padrão que entraria em vigor quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criasse uma instância do CLR.  
  
 A política de nível host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma combinação de política fixa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para assemblies de sistema e política específica de usuário para assemblies de usuário.  
  
 A política fixa para assemblies do CLR e assemblies de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a eles confiança total.  
  
 A parte especificada pelo usuário da política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se baseia na especificação de um dos três recipientes de permissão para cada assembly pelo proprietário do assembly. Para obter mais informações sobre as permissões de segurança listadas abaixo, consulte o SDK do .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Somente a computação interna e o acesso a dados local são permitidos. **Safe** é o conjunto de permissões mais restritivo. O código executado por um assembly com permissões **seguras** não pode acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou o registro.  
  
 Os assemblies **seguros** têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Execução:** Permissão para executar código gerenciado.|  
|**SqlClientPermission**|**Conexão de contexto = true**, **conexão de contexto = Sim**: somente a conexão de contexto pode ser usada e a cadeia de conexão só pode especificar um valor de "context connection = true" ou "context connection = yes".<br /><br /> **AllowBlankPassword = false:**  Senhas em branco não são permitidas.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS assemblies têm as mesmas permissões que os assemblies **seguros** , com a capacidade adicional de acessar recursos externos do sistema, como arquivos, redes, variáveis ambientais e o registro.  
  
 **EXTERNAL_ACCESS** assemblies também têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Irrestrito:** As transações distribuídas são permitidas.|  
|**DNSPermission**|**Irrestrito:** Permissão para solicitar informações de servidores de nome de domínio.|  
|**EnvironmentPermission**|**Irrestrito:** O acesso completo às variáveis de ambiente do sistema e do usuário é permitido.|  
|**EventLogPermission**|**Administrar:** As seguintes ações são permitidas: criando uma origem de evento, lendo logs existentes, excluindo fontes de eventos ou logs, respondendo a entradas, limpando um log de eventos, ouvindo eventos e acessando uma coleção de todos os logs de eventos.|  
|**FileIOPermission**|**Irrestrito:** O acesso completo a arquivos e pastas é permitido.|  
|**KeyContainerPermission**|**Irrestrito:** O acesso completo a contêineres de chave é permitido.|  
|**NetworkInformationPermission**|**Acesso:** O ping é permitido.|  
|**RegistryPermission**|Permite direitos de leitura para **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**e **HKEY_USERS.**|  
|**SecurityPermission**|**Asserção:** Capacidade de declarar que todos os chamadores desse código têm a permissão de requisito para a operação.<br /><br /> **ControlPrincipal:** Capacidade de manipular o objeto principal.<br /><br /> **Execução:** Permissão para executar código gerenciado.<br /><br /> **SerializationFormatter:** Capacidade de fornecer serviços de serialização.|  
|**SmtpPermission**|**Acesso:** Conexões de saída para a porta 25 do host SMTP são permitidas.|  
|**SocketPermission**|**Conectar:** Conexões de saída (todas as portas, todos os protocolos) em um endereço de transporte são permitidas.|  
|**SqlClientPermission**|**Irrestrito:** O acesso completo à fonte de fontes é permitido.|  
|**StorePermission**|**Irrestrito:** Acesso completo a repositórios de certificados X. 509 é permitido.|  
|**WebPermission**|**Conectar:** Conexões de saída para recursos da Web são permitidas.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite que os assemblies tenham acesso irrestrito aos recursos, dentro e fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código em execução de dentro de um assembly **não seguro** também pode chamar código não gerenciado.  
  
 Os assemblies **não seguros** recebem **FullTrust**.  
  
> [!IMPORTANT]  
>  **Seguro** é a configuração de permissão recomendada para assemblies que executam tarefas de computação e gerenciamento de dados sem acessar recursos fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . **EXTERNAL_ACCESS** é recomendado para assemblies que acessam recursos fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . **EXTERNAL_ACCESS** assemblies por padrão são executados como a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta de serviço. É possível que **EXTERNAL_ACCESS** código represente explicitamente o contexto de segurança de autenticação do Windows do chamador. Como o padrão é executar como a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta de serviço, a permissão para executar **EXTERNAL_ACCESS** deve ser dada somente a logons confiáveis para execução como a conta de serviço. De uma perspectiva de segurança, **EXTERNAL_ACCESS** e assemblies **não seguros** são idênticos. No entanto, os assemblies do **EXTERNAL_ACCESS** fornecem várias proteções de confiabilidade e robustez que não estão em ASSEMBLIES não **seguros** . Especificar **unsafe** permite que o código no assembly execute operações ilegais no espaço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] processo e, portanto, possa comprometer a robustez e a escalabilidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como criar assemblies CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , consulte [Gerenciando assemblies de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Acessando recursos externos  
 Se um tipo definido pelo usuário (UDT), um procedimento armazenado ou outro tipo de assembly de construção for registrado com o conjunto de permissões **seguro** , o código gerenciado em execução na construção não poderá acessar recursos externos. No entanto, se os conjuntos de permissões **EXTERNAL_ACCESS** ou **não seguros** forem especificados, e o código gerenciado tentar acessar recursos externos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o aplicará as seguintes regras:  
  
|Se|Então|  
|--------|----------|  
|O contexto de execução corresponda a um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|As tentativas de acessar recursos externos são negadas, e ocorre uma exceção de segurança.|  
|O contexto de execução corresponda a um logon do Windows e seja o chamador original.|O recurso externo é acesso no contexto de segurança da conta do serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|O chamador não for o chamador original.|O acesso será negado, e ocorrerá uma exceção de segurança.|  
|O contexto de execução corresponder a um logon do Windows e o contexto da execução for o chamador original, e o chamador tiver sido representado.|O acesso usará o contexto de segurança do chamador, não a conta de serviço.|  
  
## <a name="permission-set-summary"></a>Resumo do conjunto de permissões  
 O gráfico a seguir resume as restrições e permissões concedidas aos conjuntos de permissão seguro, **EXTERNAL_ACCESS**e **não** **seguro** .  
  
|Funcionalidade|**SAFE**|**EXTERNAL_ACCESS**|**UNSAFE**|   
|-|-|-|-|  
|Permissões de segurança de acesso ao código|Somente execução|Execução + acesso a recursos externos|Irrestrito (inclusive P/Invoke)|  
|Restrições do modelo de programação|Sim|Sim|Sem restrições|  
|Requisito de verificabilidade|Sim|Sim|Não|  
|Acesso a dados locais|Sim|Sim|Sim|  
|Capacidade de chamar código nativo|Não|Não|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Atributos de proteção do host e programação de integração CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrições do modelo de programação de integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente hospedado de CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
