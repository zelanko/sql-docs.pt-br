---
title: Configurar o Parallel Data Warehouse para cópias da tabela remota | Microsoft Docs
description: Descreve como configurar o Parallel Data Warehouse para usar o recurso de cópia da tabela remota para copiar tabelas para bancos de dados SMP SQL Server em servidores não seja de aplicação.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f71a0c67639918820bca8f6f8f38b9f354154f3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Configurar o Parallel Data Warehouse para cópias da tabela remota
Descreve como configurar o SQL Server PDW para usar o recurso de cópia da tabela remota para copiar tabelas para bancos de dados SMP SQL Server em servidores não seja de aplicação.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia da tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
Para configurar o SQL Server PDW para usar a cópia da tabela remota, você deve:  
  
-   Ter uma conta de administrador do sistema de plataforma de análise com a capacidade de fazer logon diretamente no ***appliance_domain *-AD01** e ***appliance_domain *-AD02** nós.  
  
-   Sabe o nome de host ou IP do servidor de destino.  
  
## <a name="HowToPDW"></a>Configurar o SQL Server PDW para cópia de tabela remota: atualizar nomes de Host no DNS  
O **CREATE REMOTE TABLE** instrução, usada para cópias da tabela remota, especifica o servidor de destino usando o endereço IP ou o nome do IP do sistema Windows SMP. Para usar o nome IP, você precisa adicionar entradas para resolução de nomes bem-sucedida para o servidor DNS.  
  
As etapas a seguir descrevem como atualizar o servidor DNS.  
  
1.  Faça logon no nó ativo do AD (normalmente ***appliance_domain *-AD01**).  
  
2.  Abra o Gerenciador de DNS. Isso está localizado em **ferramentas administrativas** no **iniciar** menu.  
  
3.  Use o Gerenciador de DNS para adicionar o nome do IP.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Use um encaminhador DNS para resolver nomes DNS não seja de aplicação](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
