---
title: "Grupos de disponibilidade independentes de domínio (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Availability Groups [SQL Server], domain independent
ms.assetid: 
caps.latest.revision: 
author: allanhirt
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61014dfd6113a16e37b4be9a1a06e6901abba37f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="domain-independent-availability-groups"></a>Grupos de disponibilidade independentes de domínio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Os AGs (Grupos de Disponibilidade) AlwaysOn exigem um WSFC (cluster de failover do Windows Server) subjacente. A implantação de um WSFC por meio do Windows Server 2012 R2 sempre exigiu que os servidores que fazem parte de um WSFC, também conhecidos como nós, sejam ingressados no mesmo domínio. Para obter mais informações sobre o AD DS (Active Directory Domain Services), consulte [aqui](https://technet.microsoft.com/library/cc759073(v=ws.10).aspx).

A dependência do AD DS e do WSFC é mais complexa do que já foi implantada anteriormente com uma configuração de DBM (Espelhamento de Banco de Dados), pois o DBM pode ser implantado em vários data centers usando certificados, sem nenhuma dessas dependências.  Um grupo de disponibilidade tradicional que abrange mais de um data center exige que todos os servidores sejam ingressados no mesmo domínio do Active Directory – diferentes domínios, até mesmo domínios confiáveis, não funcionam. Todos os servidores devem ser nós do mesmo WSFC. A figura a seguir mostra essa configuração. O SQL Server 2016 também tem grupos de disponibilidade distribuídos que também podem atingir essa meta de maneira diferente.


![WSFC abrangendo dois data centers conectados ao mesmo domínio][1]

O Windows Server 2012 R2 introduziu um [Cluster Desanexado do Active Directory](https://technet.microsoft.com/library/dn265970.aspx), uma forma especializada de um cluster de failover do Windows Server que pode ser usada com grupos de disponibilidade. Esse tipo de WSFC ainda exige que os nós sejam ingressados no mesmo domínio do Active Directory, mas nesse caso, o WSFC usa o DNS, não o domínio. Como um domínio ainda está envolvido, um Cluster Desanexado do Active Directory ainda não fornece uma experiência totalmente livre de domínio.

O Windows Server 2016 introduziu um novo tipo de cluster de failover do Windows Server baseado no Cluster Desanexado do Active Directory – um Cluster de Grupo de Trabalho. Um Cluster de Grupo de Trabalho permite que o SQL Server 2016 implante um grupo de disponibilidade em um WSFC que não exige o AD DS. O SQL Server exige o uso de certificados para a segurança do ponto de extremidade, assim como o cenário de espelhamento de banco de dados exige certificados.  Esse tipo de um grupo de disponibilidade é chamado de Grupo de Disponibilidade Independente de Domínio. A implantação de um grupo de disponibilidade com um Cluster de Grupo de Trabalho subjacente dá suporte às seguintes combinações de nós que farão parte do WSFC:
- Nenhum nó é ingressado em um domínio.
- Todos os nós são ingressados em domínios diferentes.
- Os nós são combinados, com uma combinação de nós ingressados no domínio e não ingressados no domínio.

A próxima figura mostra um exemplo de um Grupo de Disponibilidade Independente de Domínio no qual os nós do Data Center 1 são ingressados no domínio, mas os do Data Center 2 usam apenas o DNS. Nesse caso, defina o sufixo DNS em todos os servidores que serão nós do WSFC. Cada aplicativo e servidor que acessa o grupo de disponibilidade devem ver as mesmas informações de DNS.


![Cluster de Grupo de Trabalho com dois nós ingressados em um domínio][2]

Um Grupo de Disponibilidade Independente de Domínio não serve apenas para cenários de recuperação de desastre ou multissite. Ele pode ser implantado em um data center individual e até mesmo usado com um [Grupo de Disponibilidade Básico](basic-availability-groups-always-on-availability-groups.md) (também conhecido como um grupo de disponibilidade da Standard Edition) para fornecer uma arquitetura semelhante à que costumava ser obtida usando o Espelhamento de Banco de Dados com certificados, conforme mostrado.


![Exibição de alto nível de um AG na Standard Edition][3]

A implantação de um Grupo de Disponibilidade Independente de Domínio tem algumas advertências conhecidas:
- Os únicos tipos de testemunha disponíveis para uso com o quorum são disco e [nuvem](https://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness), o que é uma novidade no Windows Server 2016. O disco é um problema, pois é mais provável que não seja feito nenhum uso do disco compartilhado pelo grupo de disponibilidade.
- A variante do Cluster de Grupo de Trabalho subjacente de um WSFC só pode ser criada com o PowerShell, mas pode então ser administrada com o Gerenciador de Cluster de Failover.
- Se o Kerberos for necessário, você deverá implantar um WSFC padrão anexado a um domínio do Active Directory e um Grupo de Disponibilidade Independente de Domínio provavelmente não é uma opção.
- Embora um ouvinte possa ser configurado, ele deve ser registrado no DNS para ser utilizável. Conforme observado acima, não há nenhum suporte do Kerberos no ouvinte.
- Os aplicativos que se conectam ao SQL Server devem principalmente usar a autenticação do SQL Server, pois os domínios podem não existir ou podem não estar configurados para funcionar em conjunto. 
- Os certificados serão usados na configuração do grupo de disponibilidade.

## <a name="set-and-verify-the-dns-suffix-on-all-replica-servers"></a>Definir e verificar o sufixo DNS em todos os servidores de réplica

Um sufixo DNS comum é necessário para o Cluster de Grupo de Trabalho do Grupo de Disponibilidade Independente de Domínio. Para definir e verificar o sufixo DNS em cada Windows Server que hospedará uma réplica para o grupo de disponibilidade, siga estas instruções:

1. Usando o atalho Tecla Windows + X, selecione Sistema.
2. Se o nome do computador e o nome completo do computador forem iguais, isso indicará que o sufixo DNS não foi definido. Por exemplo, se o nome do computador for ALLAN, o valor do nome completo do computador não deverá ser apenas ALLAN. Ele deve ser algo como ALLAN.SQLHA.LAB. SQLHA.LAB é o sufixo DNS. O valor do Grupo de Trabalho deve indicar WORKGROUP. Se você precisar definir o sufixo DNS, selecione Alterar Configurações.
3. Na caixa de diálogo Propriedades do Sistema, clique em Alterar na guia Nome do Computador.
4. Na caixa de diálogo Alterações no Nome do Computador/Domínio, clique em Mais.
5. Na caixa de diálogo Sufixo DNS e Nome do Computador do NetBIOS, insira o sufixo DNS comum como o sufixo DNS Primário. 
6. Clique em OK para fechar a caixa de diálogo Sufixo DNS e Nome do Computador do NetBIOS.
7. Clique em OK para fechar a caixa de diálogo Alterações no Nome do Computador/Domínio.
8. Você deverá reiniciar o servidor para que as alterações entrem em vigor. Clique em OK para fechar a caixa de diálogo Alterações no Nome do Computador/Domínio.
9. Clique em Fechar para fechar a caixa de diálogo Propriedades do Sistema.
10. Você deverá reiniciar. Se você não desejar reiniciar imediatamente, clique em Reiniciar Depois; caso contrário, clique em Reiniciar Agora.
11. Depois que o servidor for reinicializado, verifique se o sufixo DNS comum está configurado, examinando o Sistema novamente.


![Configuração bem-sucedida do sufixo DNS][4]

## <a name="create-a-domain-independent-availability-group"></a>Criar um grupo de disponibilidade independente de domínio

Atualmente, a criação de um Grupo de Disponibilidade Independente de Domínio não pode ser realizada por completo com o SQL Server Management Studio. Embora a criação do Grupo de Disponibilidade Independente de Domínio seja basicamente o mesmo que a criação de um grupo de disponibilidade normal, alguns aspectos (como a criação de certificados) apenas são possíveis com o Transact-SQL. O exemplo abaixo pressupõe uma configuração do grupo de disponibilidade com duas réplicas: uma primária e uma secundária. 

1. [Usando as instruções deste link](https://blogs.msdn.microsoft.com/clustering/2015/08/17/workgroup-and-multi-domain-clusters-in-windows-server-2016/), implante um Cluster de Grupo de Trabalho composto por todos os servidores que farão parte do grupo de disponibilidade. Verifique se o sufixo DNS comum já está configurado antes de configurar o Cluster de Grupo de Trabalho.
2. [Habilite o recurso Grupos de Disponibilidade AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server) em cada instância que fará parte do grupo de disponibilidade. Isso exigirá uma reinicialização de cada instância do SQL Server.
3. Cada instância que hospedará a réplica primária exige uma chave mestra de banco de dados. Se uma chave mestra ainda não existir, execute o seguinte comando:
```
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Strong Password';
GO
```
4. Na instância que será a réplica primária, crie o certificado que será usado para conexões de entrada nas réplicas secundárias e para proteger o ponto de extremidade na réplica primária.
```
CREATE CERTIFICATE InstanceA_Cert 
WITH SUBJECT = 'InstanceA Certificate';
GO
``` 
5. Faça backup do certificado. Você também pode fornecer proteção avançada a ele com uma chave privada, se desejado. Esse exemplo não usa uma chave privada.
```
BACKUP CERTIFICATE InstanceA_Cert 
TO FILE = 'Backup_path\InstanceA_Cert.cer';
GO
```
6. Repita as Etapas 4 e 5 para criar e fazer backup dos certificados de cada réplica secundária, usando os nomes apropriados para os certificados, como InstanceB_Cert.
7. Na réplica primária, crie um logon para cada réplica secundária do grupo de disponibilidade. Esse logon receberá permissões para se conectar ao ponto de extremidade usado pelo Grupo de Disponibilidade Independente de Domínio. Por exemplo, em uma réplica chamada InstanceB:
```
CREATE LOGIN InstanceB_Login WITH PASSWORD = 'Strong Password';
GO
```
8. Em cada réplica secundária, crie um logon para a réplica primária. Esse logon receberá permissões para se conectar ao ponto de extremidade. Por exemplo, em uma réplica chamada InstanceB:
```
CREATE LOGIN InstanceA_Login WITH PASSWORD = 'Strong Password';
GO
```
9. Em todas as instâncias, crie um usuário para cada logon que foi criado. Isso será usado ao restaurar os certificados. Por exemplo, para criar um usuário para a réplica primária:
```
CREATE USER InstanceA_User FOR LOGIN InstanceA_Login;
GO
```
10. Para qualquer réplica que possa ser uma primária, crie um logon e um usuário em todas as réplicas secundárias relevantes.
11. Em cada instância, restaure os certificados para as outras instâncias que tinham um logon e um usuário criados. Na réplica primária, restaure todos os certificados da réplica secundária. Em cada secundária, restaure o certificado da réplica primária e também em qualquer outra réplica que pode ser uma primária. Por exemplo:
```
CREATE CERTIFICATE [InstanceB_Cert]
AUTHORIZATION InstanceB_User
FROM FILE = 'Restore_path\InstanceB_Cert.cer'
```
12. Crie o ponto de extremidade que será usado pelo grupo de disponibilidade em cada instância que será uma réplica. Para grupos de disponibilidade, o ponto de extremidade deve ter um tipo de DATABASE_MIRRORING. O ponto de extremidade usa o certificado criado na Etapa 4 para essa instância para autenticação. Uma sintaxe de exemplo é mostrada abaixo para a criação de um ponto de extremidade usando um certificado. Use o método de criptografia apropriado e outras opções relevantes para o ambiente. Para obter mais informações sobre as opções disponíveis, consulte [CREATE ENDPOINT (Transact-SQL)](../../../t-sql/statements/create-endpoint-transact-sql.md).
```
CREATE ENDPOINT DIAG_EP
STATE = STARTED
AS TCP (
    LISTENER_PORT = 5022,
    LISTENER_IP = ALL
)
FOR DATABASE_MIRRORING (
    AUTHENTICATION = CERTIFICATE InstanceX_Cert,
    ROLE = ALL
)
```
13. Atribua direitos a cada usuário criado nessa instância na Etapa 9 para que eles possam se conectar ao ponto de extremidade. 
```
GRANT CONNECT ON ENDPOINT::DIAG_EP TO 'InstanceX_User';
GO
```
14. Quando os certificados subjacentes e a segurança do ponto de extremidade são configurados, crie o grupo de disponibilidade usando seu método preferido. É recomendável fazer backup manualmente, copiar e restaurar o backup usado para inicializar a secundária ou usar a [propagação automática](automatically-initialize-always-on-availability-group.md). O uso do Assistente para inicializar as réplicas secundárias envolve o uso de arquivos do protocolo SMB, que talvez não funcionem ao usar um Cluster de Grupo de Trabalho não ingressado no domínio.
15. Se estiver criando um ouvinte, verifique se seu nome e endereço IP são registrados no DNS.

### <a name="next-steps"></a>Próximas etapas 

- [Usar a caixa de diálogo Assistente de Grupo de Disponibilidade (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [Usar a caixa de diálogo Novo Grupo de Disponibilidade (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Criar um grupo de disponibilidade com o Transact-SQL](create-an-availability-group-transact-sql.md)

<!--Image references-->
[1]: ./media/diag-wsfc-two-data-centers-same-domain.png
[2]: ./media/diag-workgroup-cluster-two-nodes-joined.png
[3]: ./media/diag-high-level-view-ag-standard-edition.png
[4]: ./media/diag-successful-dns-suffix.png
