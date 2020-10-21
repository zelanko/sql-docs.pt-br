---
title: Reconciliação de DNS do Active Directory e do Kubernetes em implantações de Clusters de Big Data
description: Configurar a reconciliação de DNS para um cluster de Big Data do SQL Server no modo do Active Directory
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 63a5c53e64ece7650e65414fd24ddd82d6da5324
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892456"
---
# <a name="active-directory-and-kubernetes-dns-reconciliation-in-big-data-clusters-deployments"></a>Reconciliação de DNS do Active Directory e do Kubernetes em implantações de Clusters de Big Data

Este artigo descreve alguns dos desafios e das soluções para acomodar a integração do Active Directory ao implantar BDCs (Clusters de Big Data).

## <a name="overview"></a>Visão geral

Quando o cluster de Big Data não é implantado com a integração do Active Directory, nós usamos o serviço [CoreDNS do Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/coredns/) para resoluções de DNS internas. O Kubernetes usa um domínio interno, como `<namespace>.svc.cluster.local`. Ele cria registros do tipo A (pesquisa direta) e PTR (pesquisa inversa) no servidor DNS com nomes nesse domínio.

No entanto, quando o modo do Active Directory está habilitado, surge um novo domínio com um conjunto próprio de servidores DNS. Durante a resolução de nomes interna, isso pode gerar confusão sobre qual conjunto de servidores DNS usar para pesquisas diretas e inversas.

## <a name="challenges"></a>Desafios

* Quando novos pods do Kubernetes forem implantados, entradas DNS precisarão ser adicionadas aos dois conjuntos de servidores DNS. O Kubernetes cuida do registro das entradas em seu CoreDNS. No entanto, o fluxo de trabalho de implantação do BDC é responsável por adicionar as entradas necessárias aos servidores DNS do Controlador de Domínio do Active Directory. De maneira semelhante, quando um cluster do BDC é excluído, o fluxo de trabalho precisa garantir que essas entradas sejam removidas.
* Os servidores DNS do Active Directory são externos ao cluster do Kubernetes. No entanto, o BDC tem um espaço de IP próprio dentro do Kubernetes e não pode criar registros para esse espaço de IP em um servidor DNS situado externamente, uma vez que esse espaço de IP não fica visível fora dos limites do cluster.
* Quando ocorrem eventos de failover no cluster do Kubernetes, os registros nos servidores DNS do AD também precisam ser atualizados.
* Além dos nomes de pod, os nomes de serviço do Kubernetes também precisam ser endereçáveis por meio das pesquisas de nome de domínio do AD. Isso cria um desafio adicional no DNS do Active Directory, uma vez que um nome de serviço pode ser mapeado para vários endereços IP de pod.
* Atrasos na propagação e na replicação de atualizações de registro nos servidores DNS do Active Directory da organização podem estar muito além do controle dos fluxos de trabalho de gerenciamento do BDC. Isso pode afetar a funcionalidade do BDC imediatamente após a implantação e o failover. Pelo contrário, o Kubernetes CoreDNS é mais rápido e eficiente devido à sua localidade.

## <a name="solution"></a>Solução

Para enfrentar os desafios mencionados, a solução implementada no BDC envolve um novo serviço CoreDNS interno gerenciado dentro do namespace do BDC. Esse é o único serviço DNS que os pods no namespace do BDC acessarão para resoluções de nome. A complexidade da presença de vários domínios fica oculta atrás do novo serviço do CoreDNS.

Por exemplo, no diagrama a seguir, os pods usam o servidor CoreDNS do BDC para resolver nomes. Os pods não interagem diretamente com o servidor CoreDNS do Kubernetes nem como o servidor DNS do AD. 

:::image type="content" source="media/active-directory-dns-reconciliation/bdc-ad-dns-reconciliation.png" alt-text="Os pods se conectam ao servidor CoreDNS no próprio namespace deles":::

Veja alguns dos detalhes da implementação que esclarecem como esse design funciona no BDC:

### <a name="centralized-management-of-multiple-domains"></a>Gerenciamento centralizado de vários domínios

A complexidade do que acontece nas pesquisas de nome permanece oculta atrás do serviço DNS interno de maneira centralizada. Isso evita colocar a carga do gerenciamento de vários domínios em pods individuais e simplifica o design.

### <a name="no-records-for-internal-pods-in-external-dns-servers"></a>Não há registros de pods internos em servidores DNS externos

Como resultado desse princípio de design, o BDC não precisará criar e gerenciar registros A nem PTR para pods no espaço de IP do Kubernetes em servidores DNS externos.

### <a name="no-duplication-of-records"></a>Não há duplicação de registros

Registros DNS internos em vários locais. O único armazenamento para esses registros é o CoreDNS do Kubernetes. O CoreDNS interno do BDC fará a reescrita computacional e o encaminhamento das consultas DNS para o CoreDNS do Kubernetes.

### <a name="computational-rewriting"></a>Reescrita computacional

Como o BDC não armazena nenhum registro, ele é responsável pela tradução das consultas de pesquisa direta de entrada com nomes que têm o domínio do AD para nomes com domínio do Kubernetes e por encaminhar essas consultas para o CoreDNS do Kubernetes.
Por exemplo, uma consulta de entrada para `compute-0-0.contoso.local` seria reescrita como `compute-0-0.compute-0-svc.contoso.svc.cluster.local` e essa solicitação seria encaminhada para o CoreDNS do Kubernetes.
No caso de pesquisas inversas, a solicitação é encaminhada com os IPs internos como estão para o CoreDNS do Kubernetes e, nele, é reescrita para o nome de domínio do AD antes de responder ao cliente.

### <a name="simplicity-in-pod-configurations"></a>Simplicidade nas configurações de pod

Como somente o CoreDNS do BDC interno é referenciado em /etc/resolv.conf em todos os pods do BDC, isso simplifica a exibição de rede dos pods. A complexidade ficará oculta no CoreDNS interno.

### <a name="static-and-reliable-ip-address-for-dns-service"></a>Endereço IP estático e confiável para o serviço DNS

O serviço CoreDNS que o BDC implanta terá um IP interno estático registrado que pode ser acessado de todos os pods. Isso garante que os valores em /etc/resolv.conf não precisem ser atualizados.

### <a name="service-load-balance-management-is-retained-by-kubernetes"></a>O gerenciamento do balanceamento de carga de serviço é mantido pelo Kubernetes

Quando acontecem pesquisas para serviços em vez de pods individuais, elas ainda vão para o CoreDNS do Kubernetes, portanto, o BDC não é responsável pela implementação do balanceamento de carga especialmente para o domínio do AD.

Por exemplo, se for recebida uma solicitação de pesquisa direta para `compute-0-svc.contoso.local`, ela será reescrita para ` compute-0-svc.contoso.svc.cluster`.local. Essa solicitação será encaminhada para o CoreDNS do Kubernetes e o balanceamento de carga ocorrerá nele. Uma resposta será um endereço IP para uma das várias instâncias do pool de computação (réplicas de pod).

### <a name="scalability"></a>Escalabilidade

Como o BDC não armazena nenhum registro, o CoreDNS do BDC interno pode ser dimensionado sem retenção de estado e replicação de registro entre várias réplicas. Se os registros DNS forem armazenados no BDC, a replicação do estado entre todos os pods também terá que ser feita pelo BDC.

### <a name="externally-visible-service-entries-stay-in-ad-dns"></a>As entradas de serviço visíveis externamente permanecem no DNS do AD

Para pontos de extremidade de serviço que precisam ser acessíveis para clientes fora do cluster do Kubernetes, as entradas DNS serão criadas no servidor DNS do AD conforme o BDC for implantado. O usuário digitará os nomes DNS para registro por meio dos perfis de configuração de implantação.

### <a name="self-deprovisioning"></a>Autodesprovisionamento

Após o BDC ser excluído, não há nenhum trabalho dinâmico adicional para excluir as entradas DNS quando o cluster está sendo desprovisionado. As únicas entradas no DNS remoto do Active Directory que precisam ser limpas são para serviços externos e são estáticas em número. As entradas DNS internas serão removidas automaticamente com o cluster.

## <a name="next-steps"></a>Próximas etapas

- [Implantar Clusters de Big Data do SQL Server no modo do Active Directory](active-directory-deploy.md)
- [Gerenciar o acesso ao cluster de Big Data no modo do Active Directory](active-directory-objects.md)
- [Implantar vários Clusters de Big Data do SQL Server no mesmo domínio do Active Directory](active-directory-deployment-background.md)
