---
title: Criar ou editar um grupo de servidor
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.editgroup.f1
- sql13.swb.newgroup.f1
helpviewer_keywords:
- Registered Servers [SQL Server], server groups
- server groups [SQL Server]
- groups [SQL Server], server
ms.assetid: d4a942bd-2dd1-42db-ad0e-e9a9ae5b856d
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 61b9111eb218f479a2b46636b648a5c9715d49f7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246552"
---
# <a name="create-or-edit-a-server-group-sql-server-management-studio"></a>Criar ou editar um grupo de servidores (SQL Server Management Studio)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este tópico descreve como organizar os servidores em Servidores Registrados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] criando grupos de servidores e colocando os servidores nesses grupos. Você pode criar grupos de servidores a qualquer hora em Servidores Registrados ou você pode criar grupos de servidores quando você registra servidores.  

## <a name="SSMSProcedure"></a>

### <a name="to-create-a-server-group-in-registered-servers"></a>Para criar um grupo de servidores em Servidores Registrados  

1. Em Servidores Registrados, clique em tipo de servidor na barra de ferramentas Servidores Registrados. Se Servidores Registrados não estiver visível, clique em **Servidores Registrados** no menu **Exibir** .  

2. Clique com o botão direito do mouse em um servidor ou um grupo de servidores, aponte para **Novo**e clique em **Grupo de Servidores**.  

3. Na caixa de diálogo **Novo Grupo de Servidores** , na caixa de listagem **Nome do Grupo** , digite um nome exclusivo para o grupo de servidores. O nome de grupo de servidores deve ser exclusivo para o local atual na árvore de Servidores Registrados.

4. Na caixa de listagem **Descrição do grupo** , opcionalmente digite um nome amigável que descreva o grupo de servidores, por exemplo, "Servidores financeiros para a América Latina."  

5. Na caixa **Selecionar um local para o novo grupo de servidores** , clique em um local para o grupo de servidores e então clique em **Salvar**.  

   > [!NOTE]
   > Você também pode criar um novo grupo de servidores enquanto registra um servidor clicando em **Novo Grupo**e preenchendo a caixa de diálogo **Novo Grupo** .  

## <a name="see-also"></a>Consulte Também

[Registrar servidores](../../tools/sql-server-management-studio/register-servers.md)