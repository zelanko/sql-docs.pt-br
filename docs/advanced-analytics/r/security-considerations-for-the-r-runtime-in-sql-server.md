---
title: "Considerações de segurança para o aprendizado de máquina no SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b5fba856cc40c11f218faf0a61f66ee5451aa4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>Considerações de segurança para o aprendizado de máquina no SQL Server

Este artigo lista as considerações de segurança que o administrador ou o arquiteto deve ter em mente ao usar os serviços de aprendizado de máquina.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="use-a-firewall-to-restrict-network-access-by-r"></a>Usar um firewall para restringir o acesso à rede por R

Em uma instalação padrão, uma regra de firewall do Windows é usada para bloquear todo o acesso de rede de saída dos processos de tempo de execução de R. Regras de firewall devem ser criadas para impedir que o processo de tempo de execução de R baixe pacotes ou faça outras chamadas de rede que podem ser potencialmente mal-intencionados.

Se você estiver usando um programa de firewall diferente, também pode criar regras para bloquear conexões de rede de saída para o tempo de execução de R, definindo regras para as contas de usuário local ou para o grupo representado pelo pool de contas de usuário.

É altamente recomendável que você ativar o Firewall do Windows (ou outro firewall de sua escolha) para impedir o acesso à rede irrestrito, os tempos de execução de R ou Python.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>Métodos de autenticação com suporte para contextos de computação remota

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]dá suporte a logons de autenticação integrada do Windows e SQL ao criar conexões entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um cliente de ciência de dados remotos.

Por exemplo, se você estiver desenvolvendo uma solução de R em seu laptop e executar cálculos no computador do SQL Server, você precisará criar uma fonte de dados do SQL Server no R, usando as funções **rx** e definindo uma cadeia de conexão com base em suas credenciais do Windows.

Quando você altera o _contexto de computação_ do seu laptop para o computador do SQL Server, se sua conta do Windows tem as permissões necessárias, todo o código R é executado no computador do SQL Server. Além disso, as consultas SQL executadas como parte do código R são executadas sob as suas credenciais.

Também há suporte para o uso de logons do SQL Server nesse cenário, o que exige que a instância do SQL Server seja configurado para permitir a autenticação de modo misto.

### <a name="implied-authentication"></a>Autenticação implícita

 Em geral, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] inicia o tempo de execução do script externo e executa scripts em sua própria conta. No entanto, se o tempo de execução externo faz uma chamada ODBC, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] representa as credenciais do usuário que enviou o comando para garantir que a chamada ODBC não falhar. Isso é chamado de *autenticação implícita*.
 
 > [!IMPORTANT]
 >
 > Para que a autenticação seja bem-sucedida, o grupo de usuários do Windows que contém as contas de trabalho implícita (por padrão, **SQLRUser**) deve ter uma conta no banco de dados mestre para a instância e essa conta deve receber permissões para se conectar à instância.
 > 
 > O grupo **SQLRUser** também é usado quando a execução de scripts de Python. 

## <a name="no-support-for-encryption-at-rest"></a>Não há suporte para criptografia em repouso

Não há suporte para a criptografia transparente de dados para dados enviados ou recebidos do tempo de execução do script externo. Como consequência, a criptografia em repouso **não** ser aplicado a todos os dados que você pode usar em scripts de R ou Python, dados salvos em disco ou resultados intermediários persistentes.

## <a name="resources"></a>Recursos

Para obter mais informações sobre como gerenciar o serviço e sobre como provisionar contas de usuário usadas para executar scripts R, consulte [configurar e gerenciar extensões de análise avançada](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md).

Para obter uma descrição da arquitetura de segurança, consulte:

+ [Visão geral de segurança para R](security-overview-sql-server-r.md)
+ [Visão geral de segurança para Python](../python/security-overview-sql-server-python-services.md)

