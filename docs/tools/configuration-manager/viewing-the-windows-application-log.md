---
title: Exibindo o log do aplicativo do Windows
description: Saiba como exibir e gerenciar o log de aplicativos do Windows. É possível configurar SQL Server para gravar informações de evento nesse log.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- application logs [SQL Server]
- Windows application logs [SQL Server]
- viewing Windows application logs
- errors [SQL Server], logs
- system logs [SQL Server]
- security logs [SQL Server]
- displaying Windows application logs
- logs [SQL Server], Windows application logs
ms.assetid: f9853b74-7db7-47cc-b957-e49ed5bc0a1a
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cfbe9955c07aaca9cf710efb405badee74dec1a2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880260"
---
# <a name="viewing-the-windows-application-log"></a>Exibindo o log do aplicativo do Windows
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurado para usar o log do aplicativo do Microsoft Windows, cada sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grava novos eventos nesse log. Ao contrário do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não é criado um novo log de aplicativos cada vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]é iniciada.  
  
 Exiba e gerencie o log do aplicativo do Windows usando Visualizador de Eventos do Windows ou o Visualizador de Log no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Há três logs que podem ser exibidos com Visualizador de Eventos.  
  
|Tipo de log do Windows|Descrição|  
|----------------------|-----------------|  
|Log do sistema|Registra eventos registrados pelos componentes do sistema operacional Windows. Por exemplo, a falha de um driver ou de outro componente do sistema carregados durante a inicialização é gravada no log do sistema.|  
|Log de segurança|Registra eventos de segurança, como tentativas de logon com falha. Também ajuda a localizar alterações no sistema de segurança e a identificar possíveis violações de segurança. Por exemplo, tentativas de logon no sistema podem ser gravadas no log de segurança, dependendo das definições de auditoria no Gerenciador de Usuários.<br /><br /> Somente os membros da função de servidor fixa **sysadmin** podem exibir os logs de segurança.|  
|Log do aplicativo|Registra eventos que são registrados através de aplicativos. Por exemplo, um aplicativo de banco de dados poderia registrar um erro de arquivo no log do aplicativo.|  
  
 Para obter mais informações sobre o recurso Visualizador de Eventos, como gerenciar o log do aplicativo e como compreender as informações apresentadas, consulte a documentação do Windows.  
  
 **Para exibir o log de aplicativos do Windows**  
  
 [Exibir o log de aplicativos do Windows &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
  
