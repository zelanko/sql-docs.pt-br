---
title: ClR Integração Code Access Security | Microsoft Docs
description: Para integração SQL Server CLR, a CLR suporta segurança de acesso ao código para código gerenciado, onde as permissões são concedidas a assembléias com base na identidade do código.
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
ms.openlocfilehash: 912db3acb6f6dc21952e99da31a1484a9745ed0b
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488294"
---
# <a name="clr-integration-code-access-security"></a>Segurança de acesso a código da integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O CLR (common language runtime) dá suporte a um modelo de segurança denominado segurança de acesso para código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Para obter mais informações, consulte a seção "Segurança de acesso do código" no Software Development Kit do .NET Framework.  
  
 A política de segurança que determina as permissões concedidas a assemblies é definida em três locais diferentes:  
  
-   Política de máquina: trata-se da política em vigor para todo o código gerenciado em execução na máquina na qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado.  
  
-   Política de usuário: trata-se da política em vigor para o código gerenciado hospedado por um processo. No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a política de usuário é específica da conta do Windows na qual o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está em execução.  
  
-   Política de host: trata-se da política configurada pelo host do CLR (nesse caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) em vigor para o código gerenciado em execução no host.  
  
 O mecanismo da segurança de acesso do código para o qual o CLR oferece suporte se baseia na pressuposição de que o runtime pode hospedar tanto o código totalmente confiável quanto o parcialmente confiável. Os recursos protegidos pela segurança de acesso do código do CLR costumam estar em interfaces de programação de aplicativo gerenciadas que exigem  a permissão correspondente para permitir o acesso ao recurso. A demanda para a permissão é satisfatória apenas quando todos os chamadores (no nível de assembly) na pilha de chamadas tiverem a permissão do recurso correspondente.  
  
 O conjunto de permissões da segurança de acesso do código concedidas ao código gerenciado em execução no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é a interseção do conjunto de permissões concedidas pelos três níveis de política acima. Mesmo que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conceda um conjunto de permissões a um assembly carregado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o conjunto de permissões final dado ao código do usuário pode ser restringido ainda mais com as políticas de nível do usuário e da máquina.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permissões do nível de política do host do SQL Server  
 O conjunto de permissões da segurança de acesso do código concedidas a assemblies pelo nível de política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é determinado pelo conjunto de permissões especificado durante a criação do assembly. Existem três conjuntos de permissões: **SAFE,** **EXTERNAL_ACCESS** e **UNSAFE** (especificado usando a opção **PERMISSION_SET** do CREATE ASSEMBLY [&#40;Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece um nível de política de segurança em nível de host ao CLR ao hospedá-lo; essa política é um nível de política adicional abaixo dos dois níveis de política que estão sempre em vigor. Essa política é definida para todos os domínios de aplicativo criados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essa política não se destina ao domínio de aplicativo padrão que entraria em vigor quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criasse uma instância do CLR.  
  
 A política de nível host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma combinação de política fixa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para assemblies de sistema e política específica de usuário para assemblies de usuário.  
  
 A política fixa para assemblies do CLR e assemblies de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede a eles confiança total.  
  
 A parte especificada pelo usuário da política de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se baseia na especificação de um dos três recipientes de permissão para cada assembly pelo proprietário do assembly. Para obter mais informações sobre as permissões de segurança listadas abaixo, consulte o SDK do .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Somente a computação interna e o acesso a dados local são permitidos. **SAFE** é o conjunto de permissões mais restritivo. O código executado por um conjunto com permissões **SAFE** não pode acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou registro.  
  
 **As** assembléias SAFE têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Execução:** Permissão para executar código gerenciado.|  
|**SqlClientPermission**|**Conexão de contexto = conexão de** **contexto , conexão de contexto = sim**: Somente a conexão contexto pode ser usada e a seqüência de conexão só pode especificar um valor de "context connection=true" ou "context connection=yes".<br /><br /> **AllowBlankPassword = falso:**  Senhas em branco não são permitidas.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS conjuntos têm as mesmas permissões que os conjuntos **SAFE,** com a capacidade adicional de acessar recursos externos do sistema, como arquivos, redes, variáveis ambientais e o registro.  
  
 **EXTERNAL_ACCESS** assembleias também têm as seguintes permissões e valores:  
  
|Permissão|Valor(es)/descrição|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Irrestrito:** Transações distribuídas são permitidas.|  
|**DNSPermission**|**Irrestrito:** Permissão para solicitar informações de servidores de nome de domínio.|  
|**EnvironmentPermission**|**Irrestrito:** É permitido o acesso total às variáveis do sistema e do ambiente do usuário.|  
|**EventLogPermission**|**Administrar:** As seguintes ações são permitidas: criar uma fonte de evento, ler registros existentes, excluir fontes de eventos ou logs, responder a entradas, limpar um registro de eventos, ouvir eventos e acessar uma coleção de todos os registros de eventos.|  
|**FileIOPermission**|**Irrestrito:** É permitido acesso total a arquivos e pastas.|  
|**KeyContainerPermission**|**Irrestrito:** É permitido acesso total a contêineres-chave.|  
|**NetworkInformationPermission**|**Acesso:** Pingar é permitido.|  
|**Registrypermission**|É o que **diz**a **HKEY_CLASSES_ROOT, HKEY_LOCAL_MACHINE,** **HKEY_CURRENT_USER,** **HKEY_CURRENT_CONFIG**e **HKEY_USERS.**|  
|**SecurityPermission**|**Afirmação:** Capacidade de afirmar que todos os chamadores deste código têm a permissão necessária para a operação.<br /><br /> **Principal controle:** Capacidade de manipular o objeto principal.<br /><br /> **Execução:** Permissão para executar código gerenciado.<br /><br /> **SerializaçãoMatéria:** Capacidade de fornecer serviços de serialização.|  
|**SmtpPermission**|**Acesso:** Conexões de saída para a porta de host SMTP 25 são permitidas.|  
|**SocketPermission**|**Conectar:** Conexões de saída (todas as portas, todos os protocolos) em um endereço de transporte são permitidas.|  
|**SqlClientPermission**|**Irrestrito:** É permitido acesso total à fonte de dados.|  
|**StorePermission**|**Irrestrito:** É permitido acesso total às lojas de certificados X.509.|  
|**WebPermission**|**Conectar:** Conexões de saída para recursos da Web são permitidas.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite que os assemblies tenham acesso irrestrito aos recursos, dentro e fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A execução de códigos de dentro de um conjunto **INSEGURO** também pode chamar código não gerenciado.  
  
 **Conjuntos inseguros** recebem **FullTrust**.  
  
> [!IMPORTANT]  
>  **SAFE** é a configuração de permissão recomendada para conjuntos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]executam tarefas de computação e gerenciamento de dados sem acessar recursos externos . **EXTERNAL_ACCESS** é recomendado para assembléias [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]que acessam recursos externos . **EXTERNAL_ACCESS** assembléias por padrão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são executadas como a conta do serviço. É possível que **EXTERNAL_ACCESS** código se personifique explicitamente no contexto de segurança do Windows Authentication do chamador. Uma vez que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] padrão é executar como a conta do serviço, a permissão para executar **EXTERNAL_ACCESS** só deve ser dada aos logins confiáveis para executar como a conta do serviço. Do ponto de vista da segurança, **EXTERNAL_ACCESS** e **INSÕES** são idênticas. No entanto, **EXTERNAL_ACCESS** conjuntos fornecem várias proteções de confiabilidade e robustez que não estão em conjuntos **INSEGUROS.** A especificação **insegurança** permite que o código [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na montagem realize operações ilegais contra o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]espaço do processo e, portanto, pode comprometer potencialmente a robustez e a escalabilidade de . Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]a criação de conjuntos CLR em , consulte [Gerenciando os Conjuntos de Integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Acessando recursos externos  
 Se um tipo definido pelo usuário (UDT), procedimento armazenado ou outro tipo de conjunto de construção for registrado com o conjunto de permissões **SAFE,** então a execução gerenciada de código no construto não poderá acessar recursos externos. No entanto, se os conjuntos de permissões **EXTERNAL_ACCESS** ou **INSEGURO** forem especificados e as tentativas de código gerenciadas acessarem recursos externos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplicarão as seguintes regras:  
  
|Se|Então|  
|--------|----------|  
|O contexto de execução corresponda a um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|As tentativas de acessar recursos externos são negadas, e ocorre uma exceção de segurança.|  
|O contexto de execução corresponda a um logon do Windows e seja o chamador original.|O recurso externo é acesso no contexto de segurança da conta do serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|O chamador não for o chamador original.|O acesso será negado, e ocorrerá uma exceção de segurança.|  
|O contexto de execução corresponder a um logon do Windows e o contexto da execução for o chamador original, e o chamador tiver sido representado.|O acesso usará o contexto de segurança do chamador, não a conta de serviço.|  
  
## <a name="permission-set-summary"></a>Resumo do conjunto de permissões  
 O gráfico a seguir resume as restrições e permissões concedidas aos conjuntos de permissões **SAFE**, **EXTERNAL_ACCESS**e **UNSAFE.**  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**Inseguro**|  
|**Permissões de segurança de acesso a código**|Somente execução|Execução + acesso a recursos externos|Irrestrito (inclusive P/Invoke)|  
|**Restrições do modelo de programação**|Sim|Sim|Sem restrições|  
|**Requisito de verificabilidade**|Sim|Sim|Não|  
|**Acesso a dados locais**|Sim|Sim|Sim|  
|**Capacidade de chamar código nativo**|Não|Não|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de Integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Atributos de proteção de host e programação de integração CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrições do modelo de programação de integração do CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente hospedado de CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
