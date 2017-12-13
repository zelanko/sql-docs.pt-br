---
title: Conectar-se com os Servidores Registrados e com o Pesquisador de Objetos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: d6b3911f-68b4-4483-831b-df89d6400add
caps.latest.revision: "50"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f280ca05701c1497843a1dd8caf78e166a1b98f5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-1-2---connect-with-registered-servers-and-object-explorer"></a>Lição 1-2 – Conectar-se com os Servidores Registrados e com o Pesquisador de Objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Este tutorial demonstra o uso de Servidores Registrados e do Pesquisador de Objetos.  
  
Este tutorial usa o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os exemplos de bancos de dados não são instalados por padrão. Para obter mais informações, consulte [Instalando exemplos de SQL Server e bancos de dados de exemplo](http://sqlserversamples.codeplex.com).  
  
## <a name="connecting-to-servers"></a>Conectando a servidores  
A barra de ferramentas do componente Servidores Registrados tem botões para o [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Você pode registrar um ou mais desses tipos de servidor para obter um gerenciamento conveniente. Tente o exercício a seguir para registrar o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
#### <a name="to-register-the-database"></a>Para registrar o banco de dados  
  
1.  Na barra de ferramentas Servidores Registrados, clique em **Mecanismo de Banco de Dados** , se necessário. (Já pode estar selecionado.)  
  
2.  Expanda **Mecanismo de Banco de Dados**.  
  
3.  Clique com o botão direito do mouse em **Grupos do Servidor Local**e clique em **Novo Registro do Servidor**.  
  
4.  Na caixa de diálogo **Registro de Novo Servidor** , na caixa de texto **Nome do Servidor** , digite o nome de sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Na caixa **Nome do servidor registrado** , digite [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
6.  Na guia **Propriedades da Conexão**, na lista **Conectar ao banco de dados**, selecione **\<Procurar servidor…>**.  
  
7.  Na caixa de diálogo **Procurar Bancos de Dados** , clique em **Sim**.  
  
8.  Na caixa de diálogo **Procurar Banco de Dados no Servidor** , selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]e clique em **OK**.  
  
9. Para verificar se o servidor foi registrado corretamente, clique em **Teste**.  
  
10. Na caixa de diálogo **Novo Registro do Servidor** , clique em **Salvar**.  
  
## <a name="connecting-with-object-explorer"></a>Conectando com o Pesquisador de Objetos  
Da mesma forma que os Servidores Registrados, o Pesquisador de Objetos pode estabelecer conexão com o [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
#### <a name="to-connect-with-object-explorer"></a>Para conectar com o Pesquisador de Objetos  
  
1.  Na barra de ferramentas do Pesquisador de Objetos, clique em **Conectar** para obter uma lista de possíveis tipos de conexão e selecione **Mecanismo de Banco de Dados**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , na caixa de texto **Nome do Servidor** , digite o nome de sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Clique em **Opções** e explore as escolhas.  
  
4.  Para conectar-se ao servidor, clique em **Conectar**. Se você já estiver conectado, essa ação o retornará ao Pesquisador de Objetos e definirá o foco naquele servidor.  
  
    Com o Pesquisador de Objetos, você pode administrar a Segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, a Replicação e o Database Mail. O Pesquisador de Objetos só pode administrar alguns dos recursos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e do [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Cada um desses componentes tem ferramentas especializadas adicionais.  
  
5.  No Pesquisador de Objetos, expanda a pasta **Bancos de Dados** e selecione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
    Observe que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] apresenta os bancos de dados do sistema em uma pasta separada.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Alterar o layout do ambiente](../../tools/sql-server-management-studio/lesson-1-3-change-the-environment-layout.md)  
  
  
  
