---
title: "Configurar o SQL Server PDW para cópias da tabela remota (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 496b4214-5891-404c-8237-c2a1e09db6d5
caps.latest.revision: "11"
ms.openlocfilehash: 08257e4823eed7bf86977ddca1df41eee7f8bda2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="configure-sql-server-pdw-for-remote-table-copies"></a>Configurar o SQL Server PDW para cópias da tabela remota
Descreve como configurar o SQL Server PDW para usar o recurso de cópia da tabela remota para copiar tabelas para bancos de dados SMP SQL Server em servidores não seja de aplicação.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia da tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
Para configurar o SQL Server PDW para usar a cópia da tabela remota, você deve:  
  
-   Ter uma conta de administrador do sistema de plataforma de análise com a capacidade de fazer logon diretamente no  ***appliance_domain*-AD01** e  ***appliance_domain*-AD02** nós.  
  
-   Sabe o nome de host ou IP do servidor de destino.  
  
## <a name="HowToPDW"></a>Configurar o SQL Server PDW para cópia de tabela remota: atualizar nomes de Host no DNS  
O **CREATE REMOTE TABLE** instrução, usada para cópias da tabela remota, especifica o servidor de destino usando o endereço IP ou o nome do IP do sistema Windows SMP. Para usar o nome IP, você precisa adicionar entradas para resolução de nomes bem-sucedida para o servidor DNS.  
  
As etapas a seguir descrevem como atualizar o servidor DNS.  
  
1.  Faça logon no nó ativo do AD (normalmente  ***appliance_domain*-AD01**).  
  
2.  Abra o Gerenciador de DNS. Isso está localizado em **ferramentas administrativas** no **iniciar** menu.  
  
3.  Use o Gerenciador de DNS para adicionar o nome do IP.  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Use um encaminhador DNS para resolver nomes DNS não seja de aplicação](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
