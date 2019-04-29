---
title: Segurança de acesso do código de integração de CLR | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62873735"
---
# <a name="clr-integration-code-access-security"></a>Segurança de acesso a código da integração CLR
  O CLR (common language runtime) dá suporte a um modelo de segurança denominado segurança de acesso para código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Para obter mais informações, consulte a seção "Segurança de acesso do código" no Software Development Kit do .NET Framework.  
  
 A política de segurança que determina as permissões concedidas a assemblies é definida em três locais diferentes:  
  
-   Política do computador: Esta é a política em vigor para todo o código gerenciado em execução na máquina na qual [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado.  
  
-   Política de usuário: Esta é a política em vigor para código gerenciado hospedado por um processo. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serviço está em execução.  
  
-   Política de host: Isso é a política configurada pelo host do CLR (nesse caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) que está em vigor para código gerenciado em execução nesse host.  
  
 O mecanismo da segurança de acesso do código para o qual o CLR oferece suporte se baseia na pressuposição de que o tempo de execução pode hospedar tanto o código totalmente confiável quanto o parcialmente confiável. Os recursos que são protegidos pela segurança de acesso do código CLR costumam estar em interfaces de programação de aplicativo gerenciado requirethe permissão correspondente antes de permitir o acesso ao recurso. O demandfor a permissão é atendido somente se todos os chamadores (no nível de assembly) na pilha de chamadas tiverem a permissão do recurso correspondente.  
  
 O conjunto de permissões de segurança de acesso do código que são concedidas ao código gerenciado em execução dentro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a um conjunto de permissões a um assembly carregado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o conjunto de permissões fornecido ao código do usuário final pode ser restrito ainda mais pelo o usuário e políticas de nível de máquina.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permissões do nível de política do host do SQL Server  
 O conjunto de permissões da segurança de acesso do código concedidas a assemblies pelo nível de política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é determinado pelo conjunto de permissões especificado durante a criação do assembly. Há três conjuntos de permissão: `SAFE`, `EXTERNAL_ACCESS` e `UNSAFE` (especificados usando o **PERMISSION_SET** opção de[CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)) .  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essa política não se destina ao domínio de aplicativo padrão que entraria em vigor quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criasse uma instância do CLR.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fixedpolicy para assemblies do sistema e a política especificada pelo usuário para assemblies de usuário.  
  
 A política fixa para assemblies do CLR e assemblies de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a eles confiança total.  
  
 A parte especificada pelo usuário da política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se baseia na especificação de um dos três recipientes de permissão para cada assembly pelo proprietário do assembly. Para obter mais informações sobre as permissões de segurança listadas abaixo, consulte o SDK do .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Somente a computação interna e o acesso a dados local são permitidos. `SAFE` é o conjunto de permissões mais restritivo. O código executado por um assembly com as permissões `SAFE` não pode acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou Registro.  
  
 Os assemblies `SAFE` têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|`SecurityPermission`|`Execution:` permissão para executar código gerenciado.|  
|`SqlClientPermission`|`Context connection = true`, `context connection = yes`: Apenas a conexão de contexto pode ser usado e a cadeia de caracteres de conexão só pode especificar um valor de "conexão de contexto = true" ou "conexão de contexto = yes".<br /><br /> **AllowBlankPassword = false:**  Senhas em branco não são permitidas.|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Assemblies EXTERNAL_ACCESS têm as mesmas permissões que `SAFE` assemblies, com a habilidade adicional para acessar recursos externos do sistema como arquivos, redes, variáveis de ambiente e o registro.  
  
 Os assemblies `EXTERNAL_ACCESS` também têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|`Unrestricted:` Transações distribuídas são permitidas.|  
|`DNSPermission`|`Unrestricted:` Permissão para solicitar informações de servidores de nomes de domínio.|  
|`EnvironmentPermission`|`Unrestricted:` é permitido o acesso completo ao sistema e às variáveis de ambiente do usuário.|  
|`EventLogPermission`|`Administer:` As seguintes ações são permitidas: criar uma origem do evento, ler logs existentes, excluir origens do evento ou logs, responder a consultas, limpar um log de eventos, escutar eventos e acessar uma coleção de todos os logs de eventos.|  
|`FileIOPermission`|`Unrestricted:` é permitido o acesso completo a arquivos e pastas.|  
|`KeyContainerPermission`|`Unrestricted:` é permitido o acesso completo a contêineres de chave.|  
|`NetworkInformationPermission`|`Access:` é permitida a execução de ping.|  
|`RegistryPermission`|Ela permite a leitura de direitos para `HKEY_CLASSES_ROOT`, `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, `HKEY_CURRENT_CONFIG` e `HKEY_USERS.`|  
|`SecurityPermission`|`Assertion:` possibilidade de declarar que todos os chamadores do código tenham a permissão necessária à operação.<br /><br /> `ControlPrincipal:` possibilidade de manipular o objeto principal.<br /><br /> `Execution:` permissão para executar código gerenciado.<br /><br /> `SerializationFormatter:` possibilidade de fornecer serviços de serialização.|  
|**SmtpPermission**|`Access:` são permitidas conexões de saída com a porta de host SMTP 25.|  
|`SocketPermission`|`Connect:` são permitidas conexões de saída (todas as portas, todos os protocolos) em um endereço de transporte.|  
|`SqlClientPermission`|`Unrestricted:` é permitido o acesso completo à fonte de dados.|  
|`StorePermission`|`Unrestricted:` é permitido o acesso completo a repositórios de certificados X.509.|  
|`WebPermission`|`Connect:` são permitidas conexões de saída com recursos da Web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite que os assemblies tenham acesso irrestrito aos recursos, dentro e fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código em execução em um assembly `UNSAFE` também pode chamar código não gerenciado.  
  
 Os assemblies `UNSAFE` recebem `FullTrust`.  
  
> [!IMPORTANT]  
>  A opção `SAFE` é a configuração de permissão recomendada para assemblies que executam tarefas de computação e de gerenciamento de dados sem acessar recursos externos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. `EXTERNAL_ACCESS` assemblies por padrão são executados como a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta de serviço, permissão para executar `EXTERNAL_ACCESS` só deve ser dada a logons confiados para execução como a conta de serviço. De uma perspectiva da segurança, os assemblies `EXTERNAL_ACCESS` e `UNSAFE` são idênticos. No entanto, os assemblies `EXTERNAL_ACCESS` fornecem várias proteções de confiabilidade e eficiência que não se encontram nos assemblies `UNSAFE`. Especificando `UNSAFE` permite que o código do assembly execute operações ilegais no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como criar assemblies do CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Gerenciando Assemblies de integração de CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Segurança da integração CLR](clr-integration-security.md)   
 [Atributos de proteção de host e programação da integração CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrições do modelo de programação de integração de CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente hospedado de CLR](../clr-integration-architecture-clr-hosted-environment.md)  
  
  
