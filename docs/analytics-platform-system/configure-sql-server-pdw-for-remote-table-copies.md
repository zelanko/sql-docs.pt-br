---
title: Cópias de tabela remota
description: Descreve como configurar o data warehouse paralelo para usar o recurso de cópia de tabela remota para copiar tabelas para bancos de dados do SMP SQL Server em servidores que não são de dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401260"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Configurar data warehouse paralelos para cópias de tabelas remotas
Descreve como configurar o SQL Server PDW para usar o recurso de cópia de tabela remota para copiar tabelas para bancos de dados do SMP SQL Server em servidores que não são de dispositivo.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia de tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
Para configurar SQL Server PDW para usar a cópia de tabela remota, você deve:  
  
-   Ter uma conta de administrador do sistema de plataforma de análise com a capacidade de fazer logon diretamente nos nós <strong> *appliance_domain*-AD01</strong> e <strong> *appliance_domain*-AD02</strong> .  
  
-   Conheça o nome do host ou o nome IP do servidor de destino.  
  
## <a name="HowToPDW"></a>Configurar SQL Server PDW para cópia de tabela remota: atualizar nomes de host no DNS  
A instrução **Create remota Table** , usada para cópias de tabelas remotas, especifica o servidor de destino usando o endereço IP ou o nome IP do sistema SMP Windows. Para usar o nome do IP, você precisa adicionar entradas para a resolução de nomes bem-sucedida no servidor DNS.  
  
As etapas a seguir descrevem como atualizar o servidor DNS.  
  
1.  Faça logon no nó ativo do AD (normalmente <strong> *appliance_domain*-AD01</strong>).  
  
2.  Abra o Gerenciador de DNS. Isso está localizado em **Ferramentas administrativas** no menu **Iniciar** .  
  
3.  Use o Gerenciador DNS para adicionar o nome do IP.  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Usar um encaminhador DNS para resolver nomes DNS que não são de dispositivo](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
