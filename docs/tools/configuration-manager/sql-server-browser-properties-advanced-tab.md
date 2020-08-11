---
title: Propriedades do Navegador do SQL Server (guia Avançado)
description: Saiba mais sobre as opções na guia Avançado na caixa de diálogo Propriedades do SQL Server Browser, como o diretório de despejo e a ID da instância.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ba79137a-cb72-4bf3-a650-e11d02cfce10
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: fa4bcec5a702b604212a465d8f3b115348e8cc87
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880340"
---
# <a name="sql-server-browser-properties-advanced-tab"></a>Propriedades do Navegador do SQL Server (guia Avançado)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  O programa Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado como um serviço no servidor. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser escuta as solicitações de entrada de recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
## <a name="options"></a>Opções  
 **Clusterizado**  
 Indica se este serviço for instalado como um recurso de um servidor clusterizado.  
  
 **Relatório de Comentários do Cliente**  
 Indica se o Monitoramento da Qualidade do Serviço foi habilitado neste serviço. Para obter mais informações sobre o Relatório de Comentários do Cliente, pesquise "Configurações de relatório de erro e uso" nos Manuais Online.  
  
 **Diretório de Despejo**  
 O local em que os despejos de memória são colocadas no caso de um erro.  
  
 **Relatório de Erros**  
 Quando definido como **Sim**, o programa Dr. Watson encaminhará informações para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou para o servidor de erro, se ocorrer uma falha grave. Para obter mais informações sobre o Relatório de Erros, pesquise "Configurações de relatório de erro e uso" nos Manuais Online.  
  
 **ID da Instância**  
 Indica a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usou essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A instância padrão é **MSSQL10_50.MSSQLSERVER**.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
