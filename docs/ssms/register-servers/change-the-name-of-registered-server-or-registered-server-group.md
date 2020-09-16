---
description: Alterar o nome de um servidor registrado ou de um grupo de servidores registrados
title: Altere o nome de um servidor registrado ou grupo de servidores
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/02/2016
ms.openlocfilehash: 28ed9e04486fe587ea3bd25d6659283846a6fa8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491789"
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>Alterar o nome de um servidor registrado ou de um grupo de servidores registrados

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este tópico descreve como exibir ou alterar o nome de um servidor registrado ou grupo de servidores no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O nome pode ser alterado a qualquer momento. Alterar o nome de um servidor nos Servidores Registrados altera apenas como o nome é exibido. Para conectar-se a um servidor diferente, você deve editar as propriedades de conexão do servidor registrado.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

No menu, procure **Exibir\\Servidores Registrados** para abrir o painel **Servidores Registrados**.

### <a name="to-change-the-name-of-a-server"></a>Para alterar o nome de um servidor

1. Em **Servidores Registrados**, expanda **Mecanismo de Banco de Dados** e **Grupos do Servidores Locais**.  

2. Clique com o botão direito do mouse em um servidor e selecione **Propriedades** para abrir a janela de diálogo **Editar Propriedades de Registro do Servidor** .

3. Na caixa de texto **Nome do servidor registrado** , digite o novo nome para o registro do servidor e clique em **Salvar**.  

### <a name="to-change-the-name-of-a-server-group"></a>Para alterar o nome de um grupo de servidores  

1. Em **Servidores Registrados**, expanda **Mecanismo de Banco de Dados** e **Grupos do Servidores Locais**.  

2. Clique com o botão direito do mouse em um grupo de servidores e selecione **Propriedades** para abrir a janela de diálogo **Editar Propriedades do Grupo de Servidores** . 

3. Na caixa de texto **Nome do grupo** , digite o novo nome para o grupo de servidores e clique em **Salvar**.  

## <a name="see-also"></a>Consulte Também

[Alterar um registro do servidor &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)
