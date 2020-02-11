---
title: Segurança de acesso ao código de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d829ef131bc8772ce2d84391513ffa52b2f2ff1a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62873735"
---
# <a name="clr-integration-code-access-security"></a>Segurança de acesso a código da integração CLR
  O CLR (common language runtime) dá suporte a um modelo de segurança denominado segurança de acesso para código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Para obter mais informações, consulte a seção "Segurança de acesso do código" no Software Development Kit do .NET Framework.  
  
 A política de segurança que determina as permissões concedidas a assemblies é definida em três locais diferentes:  
  
-   Política de máquina: trata-se da política em vigor para todo o código gerenciado em execução na máquina na qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado.  
  
-   Política de usuário: trata-se da política em vigor para o código gerenciado hospedado por um processo. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o serviço está em execução.  
  
-   Política de host: trata-se da política configurada pelo host do CLR (nesse caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) em vigor para o código gerenciado em execução no host.  
  
 O mecanismo da segurança de acesso do código para o qual o CLR oferece suporte se baseia na pressuposição de que o runtime pode hospedar tanto o código totalmente confiável quanto o parcialmente confiável. Os recursos protegidos pela segurança de acesso ao código CLR são normalmente encapsulados por interfaces de programação de aplicativo gerenciadas que requirethem a permissão correspondente antes de permitir o acesso ao recurso. O Demandfor a permissão será satisfeita somente se todos os chamadores (no nível do assembly) na pilha de chamadas tiverem a permissão de recurso correspondente.  
  
 O conjunto de permissões de segurança de acesso ao código que são concedidas ao código [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerenciado durante a execução dentro concede um conjunto de permissões [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]a um assembly carregado no, o conjunto eventual de permissões dadas ao código do usuário pode ser restringido ainda mais pelas políticas no nível do usuário e da máquina.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permissões do nível de política do host do SQL Server  
 O conjunto de permissões da segurança de acesso do código concedidas a assemblies pelo nível de política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é determinado pelo conjunto de permissões especificado durante a criação do assembly. Há três conjuntos de permissões: `SAFE` `EXTERNAL_ACCESS` e `UNSAFE` (especificado usando a opção **PERMISSION_SET** de[Create assembly &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essa política não se destina ao domínio de aplicativo padrão que entraria em vigor quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criasse uma instância do CLR.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fixedpolicy para assemblies de sistema e política especificada pelo usuário para assemblies de usuário.  
  
 A política fixa para assemblies do CLR e assemblies de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a eles confiança total.  
  
 A parte especificada pelo usuário da política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se baseia na especificação de um dos três recipientes de permissão para cada assembly pelo proprietário do assembly. Para obter mais informações sobre as permissões de segurança listadas abaixo, consulte o SDK do .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Somente a computação interna e o acesso a dados local são permitidos. 
  `SAFE` é o conjunto de permissões mais restritivo. O código executado por um assembly com as permissões `SAFE` não pode acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou Registro.  
  
 Os assemblies `SAFE` têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|`SecurityPermission`|
  `Execution:` permissão para executar código gerenciado.|  
|`SqlClientPermission`|
  `Context connection = true`, `context connection = yes`: apenas a conexão de contexto pode ser usada, e a cadeia de conexão só pode especificar um valor igual a "context connection=true" ou "context connection=yes".<br /><br /> **AllowBlankPassword = false:**  Senhas em branco não são permitidas.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS assemblies têm as mesmas permissões que `SAFE` os assemblies, com a capacidade adicional de acessar recursos externos do sistema, como arquivos, redes, variáveis ambientais e o registro.  
  
 Os assemblies `EXTERNAL_ACCESS` também têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|`Unrestricted:`As transações distribuídas são permitidas.|  
|`DNSPermission`|`Unrestricted:`Permissão para solicitar informações de servidores de nome de domínio.|  
|`EnvironmentPermission`|
  `Unrestricted:` é permitido o acesso completo ao sistema e às variáveis de ambiente do usuário.|  
|`EventLogPermission`|
  `Administer:` As seguintes ações são permitidas: criar uma origem do evento, ler logs existentes, excluir origens do evento ou logs, responder a consultas, limpar um log de eventos, escutar eventos e acessar uma coleção de todos os logs de eventos.|  
|`FileIOPermission`|
  `Unrestricted:` é permitido o acesso completo a arquivos e pastas.|  
|`KeyContainerPermission`|
  `Unrestricted:` é permitido o acesso completo a contêineres de chave.|  
|`NetworkInformationPermission`|
  `Access:` é permitida a execução de ping.|  
|`RegistryPermission`|Ela permite a leitura de direitos para `HKEY_CLASSES_ROOT`, `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, `HKEY_CURRENT_CONFIG` e `HKEY_USERS.`|  
|`SecurityPermission`|
  `Assertion:` possibilidade de declarar que todos os chamadores do código tenham a permissão necessária à operação.<br /><br /> 
  `ControlPrincipal:` possibilidade de manipular o objeto principal.<br /><br /> 
  `Execution:` permissão para executar código gerenciado.<br /><br /> 
  `SerializationFormatter:` possibilidade de fornecer serviços de serialização.|  
|**SmtpPermission**|
  `Access:` são permitidas conexões de saída com a porta de host SMTP 25.|  
|`SocketPermission`|
  `Connect:` são permitidas conexões de saída (todas as portas, todos os protocolos) em um endereço de transporte.|  
|`SqlClientPermission`|
  `Unrestricted:` é permitido o acesso completo à fonte de dados.|  
|`StorePermission`|
  `Unrestricted:` é permitido o acesso completo a repositórios de certificados X.509.|  
|`WebPermission`|
  `Connect:` são permitidas conexões de saída com recursos da Web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite que os assemblies tenham acesso irrestrito aos recursos, dentro e fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código em execução em um assembly `UNSAFE` também pode chamar código não gerenciado.  
  
 Os assemblies `UNSAFE` recebem `FullTrust`.  
  
> [!IMPORTANT]  
>  A opção `SAFE` é a configuração de permissão recomendada para assemblies que executam tarefas de computação e de gerenciamento de dados sem acessar recursos externos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. `EXTERNAL_ACCESS`os assemblies por padrão são executados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como a conta de serviço, `EXTERNAL_ACCESS` a permissão para executar deve ser dada somente a logons confiáveis para execução como a conta de serviço. De uma perspectiva da segurança, os assemblies `EXTERNAL_ACCESS` e `UNSAFE` são idênticos. No entanto, os assemblies `EXTERNAL_ACCESS` fornecem várias proteções de confiabilidade e eficiência que não se encontram nos assemblies `UNSAFE`. Especificar `UNSAFE` permite que o código no assembly execute operações ilegais em relação ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como criar assemblies [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]CLR no, consulte [Gerenciando ASSEMBLIES de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Acessando recursos externos  
 Caso uma UDT (tipo definido pelo usuário), um procedimento armazenado ou outro tipo de construção seja registrado com o conjunto de permissões `SAFE`, o código gerenciado em execução na construção não pode acessar recursos externos. No entanto, caso os conjuntos de permissões `EXTERNAL_ACCESS` ou `UNSAFE` sejam especificados e o código gerenciado tente acessar recursos externos, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica as seguintes regras:  
  
|Se|Então|  
|--------|----------|  
|O contexto de execução corresponda a um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|As tentativas de acessar recursos externos são negadas, e ocorre uma exceção de segurança.|  
|O contexto de execução corresponda a um logon do Windows e seja o chamador original.|O recurso externo é acesso no contexto de segurança da conta do serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|O chamador não for o chamador original.|O acesso será negado, e ocorrerá uma exceção de segurança.|  
|O contexto de execução corresponder a um logon do Windows e o contexto da execução for o chamador original, e o chamador tiver sido representado.|O acesso usará o contexto de segurança do chamador, não a conta de serviço.|  
  
## <a name="permission-set-summary"></a>Resumo do conjunto de permissões  
 O gráfico a seguir resume as restrições e as permissões concedidas aos conjuntos de permissões `SAFE`, `EXTERNAL_ACCESS` e `UNSAFE`.  
  
|||||  
|-|-|-|-|  
||`SAFE`|`EXTERNAL_ACCESS`|`UNSAFE`|  
|`Code Access Security Permissions`|Somente execução|Execução + acesso a recursos externos|Irrestrito (inclusive P/Invoke)|  
|`Programming model restrictions`|Sim|Sim|Sem restrições|  
|`Verifiability requirement`|Sim|Sim|Não|  
|`Local data access`|Sim|Sim|Sim|  
|`Ability to call native code`|Não|Não|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de integração CLR](clr-integration-security.md)   
 [Atributos de proteção do host e programação de integração CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrições do modelo de programação de integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente hospedado de CLR](../clr-integration-architecture-clr-hosted-environment.md)  
  
  
