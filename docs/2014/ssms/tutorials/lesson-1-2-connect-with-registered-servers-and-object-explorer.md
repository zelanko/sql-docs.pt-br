---
title: Conectar-se com os Servidores Registrados e com o Pesquisador de Objetos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6b3911f-68b4-4483-831b-df89d6400add
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9318b97ca72c7eadc7b938d984fb0a824dc4bb9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198186"
---
# <a name="connect-with-registered-servers-and-object-explorer"></a>Conectar com os Servidores Registrados e o Pesquisador de Objetos
  Este tutorial demonstra o uso de Servidores Registrados e do Pesquisador de Objetos.  
  
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
 [Alterar o layout do ambiente](lesson-1-3-change-the-environment-layout.md)  
  
  
