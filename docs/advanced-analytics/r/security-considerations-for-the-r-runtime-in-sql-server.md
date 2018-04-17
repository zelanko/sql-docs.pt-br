---
title: Considerações de segurança para o aprendizado de máquina no SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c8aa787088873adff5256208636063ba6f59b8b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>Considerações de segurança para o aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo lista as considerações de segurança que o administrador ou o arquiteto deve ter em mente ao usar os serviços de aprendizado de máquina.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

## <a name="use-a-firewall-to-restrict-network-access"></a>Usar um firewall para restringir o acesso à rede

Em uma instalação padrão, uma regra de firewall do Windows é usada para bloquear todo o acesso de rede de saída de processos externos em tempo de execução. Regras de firewall devem ser criadas para impedir que os processos de tempo de execução externa baixando pacotes ou fazer outras chamadas de rede que podem ser potencialmente mal-intencionados.

Se você estiver usando um programa de firewall diferente, você também pode criar regras para bloquear a conexão de rede de saída para tempos de execução externos, definindo regras para as contas de usuário local ou para o grupo representado pelo pool de conta de usuário.

É altamente recomendável que você ativar o Firewall do Windows (ou outro firewall de sua escolha) para impedir o acesso à rede irrestrito, os tempos de execução de R ou Python.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>Métodos de autenticação com suporte para contextos de computação remota

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] dá suporte a logons de autenticação integrada do Windows e SQL ao criar conexões entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um cliente de ciência de dados remotos.

Por exemplo, digamos que você está desenvolvendo uma solução R no seu laptop e executar cálculos no computador do SQL Server. Você precisará criar uma fonte de dados do SQL Server no R, usando o **rx** funções e definir uma cadeia de caracteres de conexão com base em suas credenciais do Windows.

Quando você altera o _contexto de computação_ do seu laptop para o computador do SQL Server, todo o código R é executado no computador do SQL Server, se sua conta do Windows tem as permissões necessárias. Além disso, as consultas SQL executadas como parte do código R são executadas sob as suas credenciais.

Também há suporte para o uso de logons do SQL Server neste cenário. No entanto, isso requer que a instância do SQL Server configurada para permitir a autenticação de modo misto.

### <a name="implied-authentication"></a>Autenticação implícita

 Em geral, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] inicia o tempo de execução do script externo e executa scripts em sua própria conta. No entanto, se o tempo de execução externo faz uma chamada ODBC, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] representa as credenciais do usuário que enviou o comando para garantir que a chamada ODBC não falhar. Isso é chamado de *autenticação implícita*.
 
 > [!IMPORTANT]
 > Para autenticação implícita seja bem-sucedida, o grupo de usuários do Windows que contém as contas de trabalho (por padrão, **SQLRUserGroup**) deve ter uma conta no banco de dados mestre para a instância e essa conta devem receber permissões para Conecte-se à instância.
 > 
 > O grupo **SQLRUserGroup** também é usado quando a execução de scripts de Python. 

Em geral, é recomendável mover grandes conjuntos de dados no SQL Server com antecedência, em vez de tentar ler os dados usando RODBC ou outra biblioteca. Além disso, use uma consulta do SQL Server ou o modo de exibição como sua fonte de dados principal, para melhorar o desempenho. 

Por exemplo, você pode obter seus dados de treinamento (normalmente os dados de maior) do SQL Server e obter uma lista de fatores de uma fonte externa. Você pode definir um servidor vinculado para obter dados da maioria das fontes de dados ODBC. Para obter mais informações, consulte [criar um servidor vinculado](https://docs.microsoft.com/sql/relational-databases/linked-servers/create-linked-servers-sql-server-database-engine).

Para minimizar a dependência em chamadas ODBC para fontes de dados externas, você também pode executar engenharia de dados como um processo separado e salvar os resultados em uma tabela ou usar o T-SQL. Consulte este tutorial para um bom exemplo de engenharia de dados no SQL vs. R: [criar recursos de dados usando o T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md).

## <a name="no-support-for-encryption-at-rest"></a>Não há suporte para criptografia em repouso

[Criptografia de dados transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption) não há suporte para dados enviados ou recebidos do tempo de execução do script externo. O motivo é que R (ou Python) é executado fora do processo do SQL Server; Portanto, dados usados pelo tempo de execução externo não são protegidos pelos recursos de criptografia do mecanismo de banco de dados.  Esse comportamento não é diferente de qualquer outro cliente em execução no computador do SQL Server que lê dados do banco de dados e faz uma cópia.

Como consequência, TDE **não** aplicado a todos os dados que você pode usar nos scripts de R ou Python ou dados salvos em disco, ou resultados intermediários persistentes. No entanto, outros tipos de criptografia, como criptografia de BitLocker do Windows ou a criptografia de terceiros aplicada no nível de arquivo ou pasta, ainda se aplicam.

No caso de [sempre criptografado](https://docs.microsoft.com/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted), tempos de execução externos não têm acesso às chaves de criptografia; portanto, os dados não serão enviados para os scripts.

## <a name="resources"></a>Recursos

Para obter mais informações sobre como gerenciar o serviço e sobre como provisionar as contas de usuário usadas para executar scripts de aprendizado de máquina, consulte [configurar e gerenciar extensões de análise avançada](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md).

Para obter uma explicação da arquitetura geral de segurança, consulte:

+ [Visão geral de segurança para R](security-overview-sql-server-r.md)
+ [Visão geral de segurança para Python](../python/security-overview-sql-server-python-services.md)
