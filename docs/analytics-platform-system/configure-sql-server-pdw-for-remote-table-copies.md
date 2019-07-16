---
title: Configurar o Parallel Data Warehouse para cópias da tabela remota | Microsoft Docs
description: Descreve como configurar o Parallel Data Warehouse para usar o recurso de cópia de tabela remota para copiar tabelas em bancos de dados do SQL Server do SMP em servidores não seja de dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4f3abd60cb4f87abc5e6cbdc420fc6c551b0ab15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961229"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Configurar o Parallel Data Warehouse para cópias da tabela remota
Descreve como configurar o SQL Server PDW para usar o recurso de cópia de tabela remota para copiar tabelas em bancos de dados do SQL Server do SMP em servidores não seja de dispositivo.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia de tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia de tabela remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
Para configurar o SQL Server PDW para usar a cópia de tabela remota, você deve:  
  
-   Ter uma conta de administrador do Analytics Platform System com a capacidade de fazer logon diretamente para o  <strong>*appliance_domain*-AD01</strong> e  <strong>*appliance_domain*-AD02</strong> nós.  
  
-   Sabe o nome de host ou IP do servidor de destino.  
  
## <a name="HowToPDW"></a>Configure o SQL Server PDW para cópia de tabela remota: Atualizar nomes de Host no DNS  
O **CREATE REMOTE TABLE** instrução, usada para cópias da tabela remota, especifica o servidor de destino usando o endereço IP ou o nome do IP do sistema Windows SMP. Para usar o nome do IP, você precisará adicionar entradas para resolução de nomes bem-sucedida para o servidor DNS.  
  
As etapas a seguir descrevem como atualizar o servidor DNS.  
  
1.  Faça logon no nó ativo do AD (normalmente  <strong>*appliance_domain*-AD01</strong>).  
  
2.  Abra o Gerenciador de DNS. Isso está localizado sob **ferramentas administrativas** na **iniciar** menu.  
  
3.  Use o Gerenciador de DNS para adicionar o nome do IP.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Usar um encaminhador DNS para resolver nomes DNS não seja de dispositivo](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
